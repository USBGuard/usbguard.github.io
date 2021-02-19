---
layout: post
title: "Increasing compiler version to C++17"
author: Zoltan Fridrich <zfridric@redhat.com>
date: 2021-03-01 11:00:00+02:00
comments: true
sitemap:
  lastmod: 2021-03-01 11:00:00+02:00
  priority: 0.5
  changefreq: monthly
  exclude: 'no'
---

As development packages are getting updated with latest features requiring newer versions of C++, we had to make a choice. We can either stuck with the old packages or start using new releases. After some investigation of newer C++ standards and its incompatibilities a decision has been made to increase the overall C++ version of USBGuard from C++11 to C++17. What does this mean for you? From now on, you will require a compiler that supports C++17 to be able to compile USBGuard sources. However, USBGuard will continue to work with old dependencies but will also support the newest development packages. An example of such package is [PEGTL](https://github.com/taocpp/PEGTL/releases/tag/3.2.0) of version 3 which uses C++17.
