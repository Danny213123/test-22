---
blogpost: true
blog_title: "The Instinct GPU Driver: Bifurcation from ROCm userspace"
date: 18 Mar 2025
author: 'Saad Rahim'
thumbnail: ''
tags: Installation
category: Ecosystems and Partners
target_audience: All Instinct GPU customers are the target audience.
key_value_propositions: A fundamental shift in our software release strategy to allow users to distinguish the Instinct GPU driver from the ROCm userspace. New applications where users do not need the ROCm userspace such as K8s, ISV applications and virtualization benefit from a separate driver distribution. Existing users will see the relationship between a single Instinct driver and multiple ROCm userspace versions clearly. In addition, future open source users can clearly differentiate upstream AMDGPU drivers from AMD's Instinct driver distribution.
language: English
myst:
    html_meta:
        "author": "Saad Rahim"
        "description lang=en": "A fundamental shift in our software release strategy to allow users to distinguish the Instinct GPU driver from the ROCm userspace. New applications where users do not need the ROCm userspace such as K8s, ISV applications and virtualization benefit from a separate driver distribution. Existing users will see the relationship between a single Instinct driver and multiple ROCm userspace versions clearly. In addition, future open source users can clearly differentiate upstream AMDGPU drivers from AMD's Instinct driver distribution."
        "keywords": "Instinct, GPU, amdgpu, ROCm, toolkit"
        "property=og:locale": "en_US"
        "amd_category": "Developer Resources"
        "amd_asset_type": "Blogs"
        "amd_blog_type": "Technical Articles & Blogs"
        "amd_technical_blog_type": "Ecosystems and Partners"
        "amd_developer_type": "Software Developer"
        "amd_deployment": "Servers"
        "amd_product_type": "Accelerators"
        "amd_developer_tool": "ROCm Software, Open-Source Tools"
        "amd_applications": "Cloud Computing"
        "amd_industries": "Data Center"
        "amd_blog_releasedate": Tues Mar 18, 12:00:00 PST 2025
---
<!---
Copyright (c) 2025 Advanced Micro Devices, Inc. (AMD)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
--->

# The Instinct GPU Driver: Bifurcation from ROCm userspace

Today ROCm is synonymous with software for AMD's Instinct GPUs. ROCm describes
everything from the driver to the runtime to the our libraries that enable AI and HPC software stacks.
Starting in ROCm 6.4, we expand our software family to include the Instinct Datacenter GPU driver.
The Instinct driver bifurcates from the current ROCm driver with a separate release process including an independent
version number scheme, a new documentation site and a laser focus on enabling applications on our datacenter GPU products.
This annoucement helps you prepare for these changes and mitigate impacts.

## What is the Instinct driver?

AMD's open source GPU driver is available through several channels. Users currently get the driver through
ROCm releases, through Radeon Software for Linux and it is present in many Linux kernel builds. The build of
the amdgpu driver and related packages currently distributed and documented with the ROCm, is now renamed as
the Instinct driver. Previously, it was referred to as the ROCm driver or ROCk. The source code of the driver
is published on ROCm/ROCK-Kernel-Driver (soon to be renamed to ROCm/instict-driver). You may ask, "This just
a renaming, why do I care?". The changes that happen with ROCm 6.4 are nomenclature related and may be ignored
without repurcussion for now. In the future, the Instinct driver will focus exclusively on the subset of features neeeded
for headless datacenter GPUs (also referred to accelerators or AI cards), i.e. GPUs without a display out. New and exciting futures are planned for the Instinct driver:

- New installation options to remove permisssion complexities such as user membership
in the video or render groups.
- Future installation options may exclude packages needed to run display outputs to reduce the driver footprint.
- A future driver release series may be maintained for security fixes for an extended period as long term stability driver.
- AMD-SMI and other system management components currently included in ROCm will transition to the Instinct driver releases in the future.

Please note that the Instinct drivers will not take steps to exclude products from other AMD GPU families although certain features may be limited by hardware capabilities.

## Why separate?

Software modularity is key to improving usability for our users. Splitting the driver makes it clear
that a single version of the driver can support software develoment with multiple versions of ROCm. This also
means you can run software built against multiple versions of ROCm without upgrading or downgrading the driver based on our Instinct driver support policy.
The Instinct driver support policy estabilishes forward and backward requirements compatiblity between the Instinct driver with ROCm toolkits. Compatiblity is maintained for ROCm toolkit
releases upto one prior to the driver release and ROCm toolkits released upto one year after the driver release.

## The transition

Separation of the software releases occurs in phases. During the ROCm 6.4 release, we create a separate
documentation site for the Instinct driver while keeping the version number for the Instinct driver synced
with ROCm. Coincinding with the ROCm 6.5 release later this year, the version numbering of the Instinct
driver release diverges from ROCm.

## Instinct driver version scheme

Package names will keep the component version numbers, in the same way as now.  We will repurpose the ROCm upgrade version field into an 8-digit field to represent the KMD version number, taking into account the point release numbering structure.  Examples of new package naming for Release 30.1.2.3:
Kernel driver: amdgpu-dkms_6.10.5.30010203-2109964.24.04_all.deb
UMD component with its own version number: libgl1-amdgpu-mesa-glx_24.3.0.30010203-2109964.24.04_i386.deb
For the meta-packages, the patch and point release numbers are also be included, for example, amdgpu-core_30.1.2.3.30010203-2109964.24.04_all.deb
Usage of version number:
The Linux download page at amd.com will use the new numbering structure.  For Release 30.1.2.3, the official name will be "Radeon SW For Linux 30.1.2.3".
The "Instinct Driver" will be referred to as "Instinct Driver 30.1.2.3".
The path in repo.radeon.com will use the new version number, for example https://repo.radeon.com/amdgpu/30.1.2.3/ .

## Common installation scenarios

Let's go over a few installation scenarios made clearer through this our nomenclature change.

### Installation of 3rd party applications

Many of our [software ecosystem application partners](link to ISV applications page) bundle ROCm binaries in their installers.
Installing ROCm is redundant in this situation. Currently, the same version number is used between ROCm userspace and ROCm driver. 
Many users end up mistakenly installing all of ROCm to enable their application. Now, the user will just install the Instinct driver and
the run the ISV installer.

### Managing a large installation with multiple ROCm versions

### Build server

•	Clearly defined options for installation combinations:
o	Instinct driver and multiple supported ROCm userspace versions
o	Instinct driver only to use with containers and ISV applications
o	ROCm userspace only for software builds and testing
o	Using the amdgpu driver bundled with Linux distributions and ROCm userspace released from AMD. Note: AMD does not validate this combination but is actively working with several Linux distributions (For blog only)  
•	Upgrade options also become more visible
o	You may upgrade your Instinct driver independently of ROCm userspace, or vice versa
o	Bug fixes in either the Instinct driver or ROCm user space maybe released independently versus the current mono-release.

## Summary

ROCm Blogs follow a consistent magazine-article approach where each blog ends with a “Summary” section.
Please provide a brief summary of your blog, reiterating the main takeaways and deliverables, as well
as what the reader learned from it.

## Disclaimers

Third-party content is licensed to you directly by the third party that owns the
content and is not licensed to you by AMD. ALL LINKED THIRD-PARTY CONTENT IS
PROVIDED “AS IS” WITHOUT A WARRANTY OF ANY KIND. USE OF SUCH THIRD-PARTY CONTENT
IS DONE AT YOUR SOLE DISCRETION AND UNDER NO CIRCUMSTANCES WILL AMD BE LIABLE TO
YOU FOR ANY THIRD-PARTY CONTENT. YOU ASSUME ALL RISK AND ARE SOLELY RESPONSIBLE
FOR ANY DAMAGES THAT MAY ARISE FROM YOUR USE OF THIRD-PARTY CONTENT.