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
Starting in ROCm 6.4, we begin the process to change our software ontology to include the Instinct Datacenter GPU driver.
This driver will bifurcate from the current ROCm with a separate release process including version number scheme, a new documentation site and a laser focus on enabling applications on our datacenter GPU products.
In short, the Instinct GPU driver enables your GPU to run applications, enables K8s and virtualization, and monitor GPU hardware and GPU processes. This annoucement delves into the changes and the impacts on our users.

With one name and version for the entire stack, we run in to communication and release issues.
What versions of ROCm userspace work with the ROCm driver version 6.4. The answer
is ROCm userspace 6.0 to ROCm userpace 6.4 work with ROCm driver 6.4. The point is same name and versioning for both the driver and userspace becomes challenging for our uses and for our documentation.
Consider a small fix in the ROCm driver that could go out tomorrow but under today's single release scheme for the driver and userspace will wait until the next release opportunity for the entire monolithic stack.

## Body

This is where you unleash your creativity. Please follow these general guidelines:

• use actionable, hands-on, conversational approach, guiding your reader through the blog and its content, maintaining engagement. Use active voice, call-to-action (CTA) text (e.g. “Interested in learning more?”, “Run this function by using”, “Try implementing this yourself”)

• keep your writing structured, engaging, and actionable. Divide the blog’s content into logical sections.

• Make sure you provide the required background and prerequisites for your blog. Outline any foundational knowledge and tools the reader will likely require.

• When describing a process use step-by-step guide, employ numbered steps or subheadings to guide the reader through the process.

• Integrate examples and use cases: provide real-world applications and scenarios. Reflect on common pitfalls and possible troubleshooting approaches, addressing potential mistakes and solutions.

Leeway into figures, equations, etc.

## Sample markdown

This section covers some markdown techniques commonly used in a blogs.

This is a table.

|      | SPX (MI300X) | CPX (MI300X) |
| ---- | :----------: | :----------: |
| NPS1 |      ✔       |      ✔       |
| NPS4 |              |      ✔       |

Below is a code snippet from the console. You can also use bash, C++, python and other languages.

```console
echo "c 226:128 rwm" > /sys/fs/cgroup/devices/devices.deny #Deny access to device 226:128 in docker (renderD128)

echo "c 226:128 rwm" > /sys/fs/cgroup/devices/devices.allow #Allow access to device 226:128 in docker (renderD128)
```

```{note}
This is how to add a note. See the [myst markdown admomition guide](https://mystmd.org/guide/admonitions) for more details.
```

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
