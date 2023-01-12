# Intro to Academy

Tags: #🧑‍🎓 
Related to: [[uname]], [[sudo]]
See also: 
Previous: [[ ]]

![[logo_intro_to_academy.png]]

This module is recommended for new users. It allows users to become acquainted with the platform and the learning process.

### Cheatsheet

| **Command** | **Description** |
| --------------|-------------------|
|`uname -a`|  Shows the current kernel and OS information |
|`sudo <command>`| Executes the command as root (Administrator) |

### Module Summary

In this module, we cover the Academy as a platform and how to use it to train yourself!

## Introduction

* * * * *

### `Welcome to HTB Academy!`
-------------------------

HTB Academy's goal is to provide a highly interactive and streamlined learning process to allow users to have fun while learning. Content within Academy is based around the concept of "guided learning". Students are presented with material in digestible chunks with examples of commands and their output throughout, not just theory. Students are provided target hosts where they can reproduce the materials presented in each section for themselves, hands-on exercises that serve as "checkpoints", and skills assessments to test their understanding of the material.

The key component of the learning process in the Academy is the `Module`. You are actually following one right now. Academy modules are designed to serve as mini standalone courses with all of the knowledge needed to complete the hands-on exercises and skills assessments taught within the module. While modules are standalone, many are related or build on each other.

* * * * *

The structure of the Academy is as follows:

#### Academy Structure

  Academy Structure

```text
Path
  ├── Module_1
  │     └── Sections
  │
  ├── Module_2
  │     └── Sections
  │
  ├── Module_3
  │     └── Sections
  │
  └── Module_4
        └── Section

```

A `Module` is split into `Sections` and a `Path` contains many modules. We will dive deeper into these meanings in the following sections.

* * * * *

### Paths
-----

`Paths` are collections of modules (i,e, a path named `Basic Toolset` may include modules on `nmap`, `sqlmap`, `Hashcat`, and other tools).

* * * * *

### Modules
-------

`Modules` always focus on specific topics or tools to help students enhance their skillset in a particular area. Many modules are scenario-based and make an effort to follow steps that would be taken in a real-world assessment to make the material extremely useful and relevant for students who are new to infosec or students looking to enhance their knowledge in a certain topic area.

* * * * *

### Sections
--------

Modules are broken down into `sections`. These sections are the "meat" of the modules and contain the subject matter being taught, relevant command output, and hands-on exercises.

* * * * *

## Sections

* * * * *

`Sections` are the smallest learning block in Academy.

We can assume that each `Section` is a page in a book, and the book itself is a `Module`.

For example, your current `Module` is Introduction to Academy and your current `Section` is Sections.

* * * * *

### Table of Contents
-----------------

You can easily navigate to the section you want via the `Table of Contents` on the right side. Your current section is always highlighted. We strongly recommend following the sections in the order that they appear.

* * * * *

### My Workstation
--------------

My Workstation is a Linux operating system (Parrot OS), pre-packed with many tools to assist you in the learning process. You can spawn it anytime from the right side menu to practice any material you are learning, and, in certain sections, you will use it to solve exercises.

* * * * *

### Interactive Sections
--------------------

You will notice that some `Sections` have a small cube icon next to them! We call these `Interactive Sections` and require one or more answers from you to complete. These `Interactive Sections` will sometimes also require the use of `My Workstation`.

By answering questions in `Interactive Sections` you are rewarded with  `Cubes`. You can use these `Cubes` to unlock other modules and content in the Academy.

## Interactive Section

---

`Interactive Sections`, as stated previously, require one or more answers from you in order to complete them.

You can always skip an interactive section by clicking `Next`, although the section will remain incomplete until you submit all the correct answers.

To complete this `Interactive Section`, answer the question below.

#### Questions

>What is the name of the first section of this module? If you are using a translation solution while studying, please disable it temporarily to enter the first section's name in English.
>
>`Introduction`

## Interactive Section with Terminal

* * * * *

This `Interactive Section` also includes a Linux instance.

You can use the instance directly from below or click `Full Screen` to open a full-screen instance in a new browser window.

On the top left part of the instance window, you will see a few icons. The one you will find yourself using the most is the `bash` terminal.

Follow the steps below to complete this exercise.

1.  Click the `Start Instance` button
2.  Try to locate the `bash` terminal icon and click it!
    -   *Hint: Look for the icons in the top-left section of the instance.*
3.  Type `uname -a` and press Enter in the terminal window.
    -   *Tip: This will return some useful information about the specific flavor of the OS and its kernel.*

```text
[user1@htb]$ uname -a
...
```

#### Questions

>Based on the commands you executed, what is likely to be the operating system flavor of this instance? (case-sensitive)
>
>`parrot`

## Interactive Section with Target

---

Sometimes we need to interact with live targets to make the learning process more effective and more realistic.

Like `My Workstation`, targets are also spawned on-demand.

If a section requires interaction with a `Target`, you can spawn it from the bottom of the page, in the top part of `Questions`.

Follow the steps below to complete this exercise.

1.  Spawn your target!
2.  Spawn `My Workstation` if you haven't done so.
3.  From your workstation, open Firefox and browse to the target URL.
4.  Answer the question below.

Interactive sections within the modules will have either an accompanying Docker target, a single VM, or multiple VMs, depending on the material. After spawning the target, there are a few ways you can interact with it.

---

### Docker Target

For modules that use a Docker target, the instance will take the form of `http://<ip>:<port>` after spawning, i.e. `http://157.245.40.149:30655`. Once this image spawns, you can choose to interact with it from the provided Pwnbox, your own VM, etc. Docker images will typically spawn more quickly than VMs. Click on `Click here to spawn the target system!` to spawn the target Docker image.

![[docker_target1.png]]

---

### VM Target

Modules that have either a Windows target, Active Directory (AD) environment, require multiple hosts, or otherwise cannot be completed using a Docker image will have an accompanying VM or set of VMs. You can click to spawn this target the same way. If the target VM requires authentication, you will be provided with credentials to authenticate via `SSH`. `WinRM`, `RDP`, etc. If you are not provided with credentials, it is safe to assume that you must attack the target from an unauthenticated standpoint unless otherwise instructed. If you choose to interact with the target via the Pwnbox, you will be automatically connected to the Academy lab VPN once the Pwnbox and target VM are spawned. Click on `Click here to spawn the target system!` to spawn the target VM.

![[vm_target1.png]]

Alternatively, you can choose to download a VPN key to interact with target VMs from your own attack box. Any targets with an accompanying VPN key will have a download button next to the Cheat Sheet on the right-hand side of the first exercise box.

You can see how much time your target has left directly under the IP address information. If your target expires, becomes unusable or unstable for any reason, feel free to click the orange arrows to spawn a fresh target. Each user can spawn their own dedicated targets. Any data (i.e., tools) saved to the target will be lost when the target either expires or a new target is spawned.

#### Questions

>What is the proof text displayed in the Target website you browsed?

## Modules

* * * * *

`Modules` are aimed at teaching you a specific topic. They contain several `Sections`, and many are `Interactive`.

`Modules` can be standalone, like the one you are currently working on, or they can be part of a `Path`, which we will outline in the next section.

You can browse available modules on the [Modules](https://academy.hackthebox.com/modules) page and start training by clicking the `Start` button on each relevant module card.

All `Modules` will require a certain amount of  `Cubes` to be unlocked. As we discussed previously, you can get more by completing `Interactive Sections` or by [choosing a subscription](https://academy.hackthebox.com/billing).

* * * * *

### Module Tiers
------------

Modules are split into 5 different `Tiers`. These tiers are an easy way to group modules into distinct categories based on their cost. Notice that a high Tier doesn't necessarily equate to a high difficulty.

Tier 0 modules are `free`. There is a catch though. :) Tier 0 modules actually cost 10  cubes. However, they award the same amount by completing all questions. This is to incentivize our users to complete each module.

Tier I modules cost 50  cubes and reward back to the users 10  cubes if they complete all questions.

Tier II modules cost 100  cubes and reward back to the users 20  cubes if they complete all questions.

Tier III modules cost 500  cubes and reward back to the users 100  cubes if they complete all questions.

Tier IV modules cost 1000  cubes and reward back to the users 200  cubes if they complete all questions.

* * * * *

### To-Do List
----------

You can add the modules you plan to take to your To-Do list visible in your [Dashboard](https://academy.hackthebox.com/dashboard). To add or remove a module from your To-Do list, click the heart icon located at the top right part of each module card in the [Modules](https://academy.hackthebox.com/modules) page.

* * * * *

### Stopping/Resuming
-----------------

You can stop working with a `Module` any time by simply navigating away or closing your browser. Your progress is saved every time you mark a section as complete using the `Mark Complete and Next` button.

* * * * *

### Skills Assessment
-----------------

Many but not all modules will have a final skills assessment (in addition to the in-module exercises) that must be taken to reach full completion and earn all cubes that the module awards. Skills assessments are performed against a separate target host. These assessments aim to test the students' knowledge of the material covered within the module sections and are designed to reinforce concepts presented in the module text. Depending on the module's size and the breadth and depth of the content, a skills assessment may require multiple steps and contain multiple questions. Other modules may have a skills assessment that only requires the student to perform a task (i.e., exploit a web application vulnerability) and submit a single flag.

* * * * *

### Completion
----------

A `Module` is marked complete once all the sections are marked as completed. This includes the `Interactive` sections of the module, meaning you need to submit the correct answers.

## Paths

* * * * *

`Paths` are sets of `Modules` that, combined, make up a broader topic.

`Paths` can be large "zero-to-hero" ones or smaller, more specialized ones targeting a specific set of topics. You can view what each path is about by expanding the `Modules` it contains.

Some `Paths` share modules, especially in the first steps of a path. This allows you to fast-forward a `Path` given that you already possess the required entry-level knowledge.

For example, imagine a scenario where you are interested in following two imaginary `Paths`:

-   Active Directory Attacks and Defense
-   Modern Web Attacks

Both paths would make sense to have some entry-level `Modules` to teach you the basics of Active Directory and web applications. Once you complete the first `Path`, given that the paths share the same entry-level `Modules`, you automatically save time on your second `Path` since you will start directly after the shared entry-level topics.

## Conclusion

* * * * *

By now, you should be familiar with the various aspects and layout of the Academy.

![[structure2.png]]

Start by picking your next `Module` or `Path` and happy learning!

-   Pick your next `Path` from [Paths](https://academy.hackthebox.com/paths) page.
-   Or pick your next `Module` from [Modules](https://academy.hackthebox.com/modules) page.

* * * * *

### Have fun!