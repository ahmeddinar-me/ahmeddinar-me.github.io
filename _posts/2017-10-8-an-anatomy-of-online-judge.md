---
layout: post
title:  "অনলাইন জাজ এর ব্যবচ্ছেদ"
date:   2017-10-6 00:00:31
author: Ahmed Dinar
categories: Development
tags: sandbox online-judge OS computer-security memory-management docker
---
* content
{:toc}

![diagram](/img/how-it.png)

আমরা যারা কমবেশি Competitive Programming অথবা Problem Solving এর সাথে যুক্ত, সবাই অনলাইন জাজ এর সাথে মোটামুটি ভাবে পরিচিত। কিভাবে একটা অনলাইন জাজ কাজ করে, কিভাবে কোড সাবমিট করার পর সেটা জাজ করা হয়, কিভাবে মেমোরি লিমিট, টাইম লিমিট কন্ট্রোল করা হয়  এবং আরও কিছু টপিক নিয়েই এই লেখা।



#### **অনলাইন জাজ কি?**
---
অনলাইন জাজ হল এক ধরণের অনলাইন এপ্লিকেশন (অথবা ওয়েব এপ্লিকেশন) যেখানে ইউজার কোড সাবমিট করলে অটোমেটিক ভাবে কম্পাইল করে, কম্পাইলার এরর চেক করে, কিছু হিডেন ইনপুট দিয়ে কোড রান করে, আউটপুট সেভ করে, রানটাইম এরর চেক করে, সবশেষে হিডেন আউটপুট এর সাথে ইউজার এর আউটপুট মিলিয়ে দেখে ফলাফল প্রদর্শন করে। 

![diagram](/img/judge.png){: .center-image }

অনলাইন জাজ কে কয়েকটা মডিউলে ভাগ করা যায়:

#### **কিউ (Queue)**
---
ডাটা স্ট্রাকচার এর Queue এর সাথে আমরা অনেকেই পরিচিত। অনলাইন জাজে তেমনি একটা Queue তে উইজার দের সাবমিশন গুলো রাখা হয় জাজ করার জন্য যেটাকে বলা হয় Submission Queue যেটা আমরা কোড সাবমিট করার পর প্রায়ই ``In queue`` স্ট্যাটাস হিসেবে দেখতে পাই।  কিউ এর বৈশিষ্ট্য অনুযায়ী (FIFO, First In First Out) সাবমিশন গুলো পর পর জাজ করা হয়। আমাদের মাথায় প্রশ্ন আসতে পারে কেন সবগুলো সাবমিশন কে একসাথে জাজ করা হয়না? আসলে একসাথে (concurrently) মোটামুটি ৩-৪ টা (অনলাইন জাজ ভেদে ভিন্ন হতে পারে) সাবমিশন কে জাজ করা হয়। তবে বড় কন্টেস্ট এ High Traffic কন্ট্রোল করার জন্য সংখ্যাটা বারিয়ে দেওয়া হয় যেন খুব বেশি সংখ্যক সাবমিশন অনেক বেশি সময় ধরে Queue তে অপেক্ষা না করে থাকে। বেশি সংখ্যক concurrent জাজ এর জন্য বেশি পরিমাণ [resource](https://en.wikipedia.org/wiki/System_resource) (multiple pc or high memory & processor) প্রয়োজন যেটা বেশ ব্যয়বহুল।

#### **Judger/Grader**
---
কোড কম্পাইল করা, রান করা এবং আউটপুট পরীক্ষা করা Grader এর কাজ। এটার প্রথম কাজ হল কোড কম্পাইল করা এবং Compilation Error চেক করে। যদি কোন Error না থাকে, তাহলে পরবর্তী কাজ হল কিছু ইনপুট দিয়ে কোড কে রান করা। কিন্তু এই দুইটা ধাপ অনলাইন জাজ এমনকি অনলাইন যেসব কম্পাইলার আছে (যেমন [ideone](https://ideone.com), [codepad](http://codepad.org/)), তাদের জন্য ও বড় ধরনের Security Issue.  **অনলাইন জাজ একটা প্রোগ্রাম অথবা কোড *কিভাবে কাজ করছে বা কি কাজ করছে*  তার উপর ভিত্তি না করে বরং *কি আউটপুট দিল* তার উপর ভিত্তি করে জাজ করে।** তাই আমরা আমাদের কোডে যা কিছু করিনা না কেন, সেটা জাজ সার্ভারের পিসি তে রান হবেই। একারণে সাবমিট করা কোড কে বলা হয় Untrusted Code. এটা সার্ভার পিসি এর কি কি ক্ষতি করতে পারে?
- সার্ভার পিসির গুরুত্বপূর্ণ ফাইল access এবং delete করে দিতে পারে। ছোট উদাহরণস্বরূপ C এর [rmdir()](https://linux.die.net/man/3/rmdir) এবং [unlink()](https://linux.die.net/man/2/unlink) ফাংশন ব্যাবহার করে ফোল্ডার এবং ফাইল delete করে দেওয়া যায়। আবার যদি সব ফাইল এবং ফোল্ডার read করতে পারে, তাহলে সহজেই সার্ভারে রাখা সল্যুশন ফাইল হ্যাক করা সম্ভব!
- অন্য কোন পিসি এর সাথে নেটওয়ার্ক কানেকশন ব্যাবহার করে যোগাযোগ করতে পারে। যেমন TCP/IP socket connection।
- অন্য কোন প্রোগ্রাম বা process রান করতে পারে। ছোট উদাহরণস্বরূপ C এর [exec()](http://man7.org/linux/man-pages/man3/exec.3.html) ফাংশন।

এছাড়া আরও অনেক ইস্যু আছে। Java, Python এর মত শক্তিশালী প্রোগ্রামিং ল্যাঙ্গুয়েজ গুলো ব্যবহার করে অনেক কিছুই করা সম্ভব। এখানে আরও কিছু ইস্যু পাওয়া যাবে: [What Untrusted Java Code Can't Do](http://www.securingjava.com/chapter-two/chapter-two-2.html)

এই ক্ষতি গুলো এড়াতে অনলাইন জাজ [Sandbox](https://en.wikipedia.org/wiki/Sandbox_(computer_security)) নামে একধরনের  security mechanism ব্যবহার করে থাকে।

#### **Sandbox**
---
অনেক দেশে বাচ্চাদের খেলার জন্য বড় একটা কাঠের বা প্লাস্টিকের পাত্রে বালু বা sand রাখা হয়। মোটামুটি একটা কৃত্রিম বালুকাময় পরিবেশ বাড়ির উঠোনেই তৈরি করা হয় যেন বাচ্চারা দাপাদাপি করে খেলতে পারে! এটা [sandbox বা sandpit](https://en.wikipedia.org/wiki/Sandpit) নামে পরিচিত।

![sandbox](/img/sandbox.jpg){: .sandbox-img .center-image }
[image source](https://www.parentmap.com/images/stories/Holiday_Images/0413_playspace_sandbox.jpg){: style="font-size: 12px; text-align: center; margin: 0 auto; display: block;" }

Code-Sandbox অনেকটা তেমন ই একটা সিস্টেম (OS) এর ভিতর আরেকটা কৃত্রিম সিস্টেম এর পরিবেশ তৈরি করা হয় এবং সেই কৃত্রিম সিস্টেম এ untrusted code রান করা হয়।  এই কৃত্রিম  পরিবেশ কে isolated environment বলা হয়। এই environment এ অনেক পারমিশন (file access, network etc) এবং resource (memory, time etc) লিমিট করে দেওয়া হয়। ফলে কোন untrusted code ক্ষতি করার চেষ্টা করলে ওই লিমিটেশন এর কারণে করতে পারেনা অথবা ক্ষতি করলেও মুল সিস্টেম এ তার ইফেক্ট পরবেনা। Sandboxing এর কয়েকটি সল্যুশন হতে পারে:

##### **Chroot**

chroot er পূর্ণ রূপ হল Change root. এটা দ্বারা Unix operating system এর root directory পরিবর্তন করা হয় এবং পরিবর্তন করে একটা আলাদা ডিরেক্টরির রুট access দেওয়া হয়। আমরা যারা লিনাক্সের সাথে পরিচিত, তারা নিশ্চয় দেখেছি root directory (/) তে bin, boot, etc, lib, usr ইত্যাদি ফোল্ডার থাকে। ঠিক এই রকম সব ফোল্ডার ই এই নতুন ডিরেক্টরিতে থাকে এবং আলাদা OS হিসেবে কাজ করে। chroot করে যখন ওই ডিরেক্টরিতে যাওয়া হয় তখন মুল সিস্টেম এর ফাইল বা ফোল্ডার access করা যায়না। ওই ডিরেক্টরির ভিতর আটকা পরে যায়। এই জন্য একে Chroot Jail ও বলা হয়। এটা স্বতন্ত্র ভাবে security এর জন্য খুব একটা ভালো অপশন না।


##### **System Call Interception**

প্রথমেই বলি system call কি। আমরা যারা মোটামুটি Operating System (OS) সম্পর্কে জানি, তারা kernel শব্দটার সাথে পরিচিত। Kernel হল OS এর core program যেটা সিস্টেমের hardware এবং অন্যান্য resource এবং  services (যেমন file, memory, process, network connection etc) **সরাসরি access করতে পারে**। কিন্তু উইজার প্রোগ্রাম (সংক্ষেপে আমরা যে প্রোগ্রাম লিখি!) এই resource গুলো সরাসরি ইউজ করতে পারেনা। **System call হল কোন উইজার প্রোগ্রাম এর মাধ্যমে সিস্টেম এর এই resource আর service ইউজ করার জন্য kernal এর কাছে request পাঠানো**। একটা ছোট উদাহরণ C এর [open()](http://man7.org/linux/man-pages/man2/open.2.html) system call যেটা দিয়ে ফাইল open করা যায়। আচ্ছা! তাহলে আমরা gcc এর [fopen()](http://www.cplusplus.com/reference/cstdio/fopen/) উইজ করতে পারি!! আসলে fopen হল **Library function** যা আসলে open() এর একটি wrapper বলা যায় যা শেষে open() কেই call করে। আচ্ছা তাহলে কি সব Library function ই System call এর wrapper? না। কিছু Library function system call ইউজ করে, কিছু করেনা। যেমন [strlen()](http://www.cplusplus.com/reference/cstring/strlen/) করেনা।

[এখানে Linux এর সব গুলো Systemcall এর লিস্ট পাওয়া যাবে](https://filippo.io/linux-syscall-table/)

[আরও বিস্তারিত - Library functions Vs System calls](http://www.thegeekstuff.com/2012/07/system-calls-library-functions/comment-page-1/)

তাহলে কোন প্রোগ্রামকে সিস্টেমের ক্ষতি করতে হলে অবশ্যই সিস্টেমের resource ইউজ করতে হবে, আর তার জন্য system call ব্যবহার করতে হবে! তাহলে আমারা যদি system call নিয়ন্ত্রণ করতে পারি, প্রোগ্রামও নিয়ন্ত্রণ করতে পারব। এটাকেই বলা হয় System Call Interception।  প্রোগ্রামকে একটা process এ রান করা হয় এবং এই process টি *trace বা নজরদারি* করা হয়।  এই কোডটি যদি কোন system call কল করে তাহলে kernel সেটা রান করার আগে tracing system চেক করে এটি আসলে কোন বিপদজনক system call কিনা। এটা করা যায় প্রথমে একটি white listing করে, যে লিস্ট এ থাকে safe বা allowed system call এর লিস্ট। যদি কোন system call এই লিস্টে না পাওয়া যায় তাহলে সেটা বিপদজনক!

এই System Call Interception এর উপর ভিত্তি করে বেশ কয়েকটি sanboxing solution আছে:
- [Ptrace](https://en.wikipedia.org/wiki/Ptrace)
- [Systrace](https://en.wikipedia.org/wiki/Systrace)
- [Seccomp](https://en.wikipedia.org/wiki/Seccomp)
- [Geordi](https://stackoverflow.com/a/3859784/4839437) , used by [codepad](http://codepad.org/about)
{: .list-normal }

কিছু open source systemcall tracing based sandbox:

- [EasySandbox](https://github.com/daveho/EasySandbox/blob/master/EasySandbox.c)
- [QingdaoU - Judger](https://github.com/QingdaoU/Judger/blob/master/judger.c)
- [libsandbox](https://github.com/openjudge/sandbox/blob/V_0_3_x/libsandbox/src/sandbox.c)
{: .list-normal }


##### **Linux container এবং Docker**

আমরা অনেকেই হয়ত Virtual Machine বা Virtual Box এর সাথে পরিচিত এবং Windows এর ভিতর লিনাক্স ইউজ করার জন্য হয়ত ব্যবহারও করেছি। [Linux Container বা  LXC](https://en.wikipedia.org/wiki/LXC) অনেকটা VM এর মত হলেও অনেক lightweight এবং fast. LXC মুল সিস্টেম এর kernel কে share করে সম্পূর্ণ নতুন একটি আলাদা OS হিসেবে কাজ করে। [Docker](https://www.docker.com/what-docker) হল Linux Container এর একটা implementation বা service যা খুব সহজেই Virtual OS create করতে পারে এবং destroy করে দিতে পারে মুহূর্তেই! সহজ এবং সেফ সল্যুশন এর জন্য এটা বেশ জনপ্রিয়তা পাচ্ছে।

কিছু open source docker based sandbox:
- [Compilebox](https://github.com/remoteinterview/compilebox)
- [trusted-sandbox](https://github.com/vaharoni/trusted-sandbox)
{: .list-normal }


উপরের দেওয়া sandboxing solution গুলো ছাড়াও আরও কিছু সল্যুশন আছে। [**SELinux**](https://en.wikipedia.org/wiki/Security-Enhanced_Linux) এবং [**AppArmor**](https://en.wikipedia.org/wiki/AppArmor) kernel level security দিয়ে থাকে।  [**এই পেপার টিতে**](http://mj.ucw.cz/papers/isolate.pdf) Namespaces এবং Control Group based contest sandbox নিয়ে বিস্তারিত পাওয়া যাবে। 

এই sanbox এর ভিতর যখন প্রোগ্রাম রান করা হয় এবং কোন সিকিউরিটির জন্য প্রোগ্রাম থেমে যায় তাহলে সেটা Runtime Error হিসেবে দেখায়। বেশির ভাগ অনলাইন জাজই সিকিউরিটির জন্য শুধু Runtime Error ই দেখায়, কি কারনে ইরর সেটা আমাদের কে দেখায়না।




##### **Memory Limit এবং Time Limit**
---
Memory Limit এবং Time Limit নিয়ন্ত্রণ করা sandboxing এরই একটা অংশ। কারণ কোন কোড যদি অনেক বেশি মেমরি ইউজ করে, তাহলে সার্ভার পিসি মেমরি স্বল্পতায় ক্রাশ বা হ্যং করতে পারে! তেমনি কোন কোড infinite loop তৈরি করে রান হতেই থাকলে সার্ভার পিসি অথবা জাজ হুমকি তে পরবে! আমরা অলরেডি জানি যে প্রতিটা প্রবলেমেই মেমরি আর টাইম লিমিট বলা থাকে। 

**ulimit**

লিমিট নিয়ন্ত্রণের একটা সল্যুশন হল [**ulimit**](https://docs.oracle.com/cd/E19683-01/816-0210/6m6nb7mo3/index.html) . এটা লিনাক্সের একটা কমান্ড যা কোন process এর maximum heap size, stack size, CPU time, virtual memory ইত্যাদির লিমিট নির্ধারণ করে। কোন লিমিট ক্রস করলেই এটা process টাকে terminate বা kill করে দেয়।

{% highlight cpp %}
#include <stdio.h>

int main(){
  while(1);
  return 0;
}
{% endhighlight %}

আমরা যদি উপরের কোড কে কম্পাইল এবং রান করি ulimit বাদে, তাহলে আজীবন চলতে থাকবে।

```bash
$ gcc -o code code.c
$ ./code

```

এখন ulimit দিয়ে টাইম ৩ সেকেন্ড সেট করি তারপর রান করি। তাহলে আমারা টার্মিনালে ৩ সেকেন্ড পর দেখতে পাব ``Killed``।
```bash
$ ulimit -t 3
$ ./code
Killed
$
```

**setrlimit**

ulimit এর বিকল্প হল  [setrlimit()](https://linux.die.net/man/3/setrlimit) এবং [getrlimit()](http://man7.org/linux/man-pages/man2/getrlimit.2.html) system call function. ulimit এর মতই setrlimit কোন process এর সব রকম লিমিট সেট করে তবে এটা প্রোগ্রাম এর মাধ্যমে, কমান্ড দিয়ে নয়।  নিচে CPU লিমিট এর ছোট উদাহরণ দেওয়া হল:

{% highlight cpp %}
#include <stdio.h>
#include <sys/resource.h>
#include <sys/time.h>
#include <unistd.h>

int main (){
  struct rlimit rl;

  /* সিস্টেমের default লিমিট নিবে */
  getrlimit (RLIMIT_CPU, &rl);

  /* default লিমিট কে override করে CPU লিমিট ২ সেকেন্ড সেট করবে */
  rl.rlim_cur = 2;
  setrlimit (RLIMIT_CPU, &rl);

  /* infinite loop */
  while (1);

 return 0;
}
{% endhighlight %}

প্রোগ্রামটি রান করলে ২ সেকেন্ড পর নিচের মেসেজটি দেখাবে।

```bash
CPU time limit exceeded (core dumped)
```

#### **কিভাবে Used Memory এবং Time নির্ণয় করা হয়?**
---
কোন প্রোগ্রাম কতটুকু মেমরি ইউজ করলো তা কিভাবে হিসাব করা হয় তা নিয়ে [**hackerearth এর এই লেখাটিতে**](https://www.hackerearth.com/zh/practice/notes/vivekprakash/technical-diving-into-memory-used-by-a-program-in-online-judges/) চমৎকার explanation পাওয়া যাবে। আর টাইম হিসাব নিয়ে [**quora তে same author এর এই আনসারটি**](https://www.quora.com/TopCoder/How-do-online-judges-identify-time-limit-exceeded-I-have-to-design-C%2B%2B-code-that-calls-a-function-I-must-not-run-that-function-for-more-than-2-seconds-I-must-terminate-running-that-function-if-it-exceeds-that-time) । যখন linux এ কোন একটা process রান হয়, তখন ওই process এর আইডির নামে একটা ফোল্ডার তৈরি হয় ``/proc`` directory তে। ফোল্ডারটিতে কিছু ফাইল থাকে যেগুলো ওই process এর অনেক ইনফরমেশন (যেমন virtual memory, stack, heap) সংরক্ষণ থাকে। বিস্তারিত আর লিখছি না। [আরও জানতে](http://man7.org/linux/man-pages/man5/proc.5.html) ।

#### **Standard Input/Output কি? কিভাবে ইনপুট দিয়ে প্রোগ্রাম রান করা হয়?**
---
প্রবলেমে অনেক সময় বলা থাকে এমন প্রোগ্রাম লিখতে যেটা standard input(stdin) থেকে ইনপুট রিড করবে আর standard output(stdout) এ রেসাল্ট প্রিন্ট করবে। এই stdin আর stdout আসলে কি? এটা হল প্রোগ্রাম আর সিস্টেম (যে পিসি বা OS এ প্রোগ্রাম টা রান হচ্ছে) এর ভিতর ডাটা আদান প্রদানের কানেকশন। এটা মূলত আমরা কিবোর্ড দিয়ে যে ডাটা দিব সেই ডাটা প্রোগ্রাম কে দিবে আর প্রোগ্রাম আউটপুট [console](https://en.wikipedia.org/wiki/System_console) এ প্রিন্ট করবে। আচ্ছা তাহলে জাজ এর হিডেন ইনপুট তো ফাইলে সেভ করা থাকে, তাহলে কিভাবে এটা stdin তে রূপান্তর করে? এটা করার ২টা উপায়:

##### **IO Redirection (>, <)**

Console বা Command prompt এ ``<`` operator ব্যবহার করে ফাইল এর ডাটা কে Standard Input এ redirect করা যায়। একটা উদাহরণ দিয়ে দেখানো যাক। নিচের প্রোগ্রামটি দুইটি নাম্বার ইনপুট হিসেবে নিবে আর তাদের যোগফল প্রিন্ট করবে। 

{% highlight cpp %}
#include <stdio.h>

int main(){
  int a,b;
  while( scanf("%d %d",&a,&b) == 2 ){
    printf("%d\n",a+b);
  }
  return 0;
}
{% endhighlight %}

প্রোগ্রামটি যে ফোল্ডার আ আছে সেই ফোল্ডার এ input.txt নামে একটি ফাইল তৈরি করি।

![diagram](/img/oj_input.png)

এবার এই ফোল্ডার এ console ওপেন করে নিচের মত করে রান করলে দেখতে পাব ফাইল এর ইনপুট নিয়ে যোগফল দেখাচ্ছে।

```bash
$ ./code < input.txt
10
7
```

তেমনি ``>`` operator ঠিক উল্টা কাজটা করে। এটা Standard Output কে ফাইল স্ট্রিমে redirect করে. যদি ওই নামে ফাইল না থাকে তাহলে ফাইল তৈরি করে নেয়।

```bash
$./code < input.txt > output.txt
```

![diagram](/img/oj_output.png)

##### **Duplicate File Descriptor**

File Descriptor কি? যখন কোন ফাইল ওপেন করা হয় তখন Operating System ওই ফাইল এর একটা identity দেয়, এটার জন্য সাধারণত integer ব্যবহার করা হয়। যদি অনেকগুলো ফাইল ওপেন করা থাকে তাহলে প্রতিটার জন্য আলাদা আলাদা নাম্বার দিয়ে ফাইল গুলোকে চিনহিত করা হয়, এই নাম্বার গুলোই একেকটা ফাইল এর  Descriptor। **Standard Input এবং Standard Output এর এই Descriptor নাম্বার যথাক্রমে  0 এবং 1**. [**dup2()**](http://man7.org/linux/man-pages/man2/dup.2.html) system call function একটি file descriptor এর কপি তৈরি করে। এই dup2() ফাংশন দুইটি parameter গ্রহণ করে, প্রথমটি যে file descriptor এর কপি তৈরি করা হবে, দ্বিতীয়টি নতুন যাকে দেওয়া হবে। নিচে ছোট্ট উদাহরণে উপরের প্রোগ্রামটিতে dup2 এর ব্যবহার দেখান হল:

{% highlight cpp %}
#include <stdio.h>
#include <unistd.h>
#include <fcntl.h>
 
int main(){
    //input.txt এবং output.txt ফাইল দুইটির descriptor এখন যথাক্রমে inputDesc এবং outputDesc variables
    int inputDesc = open("input.txt", O_RDWR | O_CREAT, S_IRUSR | S_IWUSR);
    int outputDesc = open("output.txt", O_RDWR | O_CREAT, S_IRUSR | S_IWUSR);

    //input.txt ফাইল এর descriptor টিকে stdin এ কপি করবে
    dup2(inputDesc, 0);

    //output.txt ফাইল এর descriptor টিকে stdout এ কপি করবে
    dup2(outputDesc, 1);
 
    int a,b;
    while( scanf("%d %d",&a,&b) == 2 ){
      printf("%d\n", a+b);
    } 
    return 0;
}
{% endhighlight %}

প্রোগ্রামটি রান করলে input.txt থেকে ইনপুট নিয়ে output.txt এ রাইট করবে। 

#### **Comparator**
---
Grader এর সর্বশেষ কাজ হল ইউজারের আউটপুটের সাথে জাজ এর হিডেন অউটপুট compare করে ফাইনাল রেসাল্ট বা verdict কি হবে সেটা নির্ণয় করা। এই জন্য একটা প্রোগ্রাম লেখা হয় যেটা দুইটা ফাইল রিড করে line by line এমনকি character by character চেক করে দেখে এবং কিছু রুলস মেনে সিদ্ধান্ত নেয় সল্যুশন ঠিক আছে কিনা। এই রুলস গুলোর ভিতর white space ignore, new line ignore ইত্যাদি থাকে। অনেক প্রবলেম এ floating point এর একটা রুলস থাকে, যার জন্য আলাদা প্রোগ্রাম দিয়ে পরীক্ষা করা হয়। এই পর্যায়ে এসে আমরা Wrong Answer, Presentation Error রেসাল্ট গুলো পেয়ে থাকি।  [**এই লিংকে**](https://github.com/DMOJ/judge/tree/master/dmoj/checkers) python এ লেখা এবং [**এই লিংকে**](https://github.com/blackav/ejudge/tree/master/checkers) C এ লেখা কয়েক প্রকার অউটপুট চেকার পাওয়া যাবে ।

#### **জাভা বৃত্তান্ত**
---
###### **Sanboxing**

Java প্রোগ্রামের সিকিউরিটির জন্য আলাদা পদ্ধতি ব্যবহার করা হয়। জাভার নিজস্ব একটি সিকিউরিটি ফিচার আছে যেটাকে বলা হয় [SecurityManager](http://docs.oracle.com/javase/7/docs/technotes/guides/security/spec/security-spec.doc6.html)। এটা একটা policy file উইজ করে যে ফাইলটিতে প্রোগ্রামটির পারমিশন গুলোর লিস্ট থাকে। যে পারমিশন গুলো বাদে অন্য কিছু করতে গেলে এই Security Manager প্রোগ্রাম টি থামিয়ে দেয় এবং পারমিশন এরর দেখায়। 


###### **Memory**

C বা C++ প্রোগ্রাম থেকে জাভা একটু ভিন্যভাবে কাজ করে বা রান হয়। C/C++ কোড কে কম্পাইল করলে সরাসরি [Binary Executable](https://en.wikipedia.org/wiki/Executable) ফাইল তৈরি করে যেটা windows এ আমরা .exe হিসেবে পাই যা ডাবল ক্লিক করে রান করা যায়, লিনাক্সে ``./filename`` দিয়ে সরাসরি রান করা যায়। জাভা প্রোগ্রামকে javac দিয়ে কম্পাইল করলে .class ফাইল তৈরি করে। এই ফাইল টি ডাবল ক্লিক করে বা কমান্ড দিয়ে সরাসরি রান করানো যায়না। এই .class ফাইলকে বলা হয় [Bytecode](https://en.wikipedia.org/wiki/Bytecode) ফাইল। এটা রান করার জন্য [Java virtual machine বা JVM](https://en.wikipedia.org/wiki/Java_virtual_machine) ব্যবহার হয়। 

প্রথমে এই JVM নিজে রান হয় এবং কিছু মেমরি বরাদ্দ বা allocate করে। তারপর প্রোগ্রামটি রান হয়। এই প্রাথমিক মেমরি এবং সর্বোচ্চ কত মেমরি JVM উইজ করতে পারবে তা কমান্ডের flag উইজ করে নির্ধারণ করা যায়। ``-Xms`` flag টি নির্ধারণ করে প্রথমে কতটুকু মেমরি JVM নিবে এবং  ``-Xmx`` নির্ধারণ করে সর্বোচ্চ কত পর্যন্ত মেমরি নিতে পারবে। এই মেমরি লিমিট আসলে JVM এর Heap Memory লিমিট. JVM এর Stack Memory লিমিট এর জন্য ``-Xss`` flag ব্যবহার করা হয়। 

Heap এবং Stack নিয়ে বেশি কিছু লিখছিনা। এই সম্পর্কে [এই লেখাটিতে](https://www.journaldev.com/4098/java-heap-space-vs-stack-memory) চমৎকার ব্যাখ্যা পাওয়া যাবে।  <a href="#বিভিন্ন-অনলাইন-জাজের-compiler-langauge-এবং-environment">নিচে</a> দেওয়া বিভিন্ন অনলাইন জাজের কম্পাইলার অপশন গুলো দেখলেই তাদের জাভার এই লিমিট গুলো সম্পর্কে জানা যাবে। [আরও](https://docs.oracle.com/cd/E15523_01/web.1111/e13814/jvm_tuning.htm#PERFM164) ।

#### **কিছু লিংক**
---
##### বিভিন্ন অনলাইন জাজের Compiler, Langauge এবং Environment
- [Toph - compilers](https://toph.co/languages)
- [Codeforces - compilers](http://codeforces.com/blog/entry/79) , [clusters](http://codeforces.com/blog/entry/8457)
- [Hackerearth - Judge Environment](https://www.hackerearth.com/docs/wiki/developers/judge/)
- [Hackerrank- Environment & Options](https://www.hackerrank.com/environment)
- [Codechef - compilers](https://discuss.codechef.com/questions/3480/what-are-the-compiler-options-that-the-judge-uses)
- [Spoj - clusters](http://www.spoj.com/clusters/)
- [AizuOJ - System information](http://judge.u-aizu.ac.jp/onlinejudge/system_info.jsp)
{: .list-normal }

##### Open Source Online Judge
- [A List in Codeforces](http://codeforces.com/blog/entry/16586)
- [The Moe Contest Environment](http://www.ucw.cz/moe/)
- [Contest Management System](http://cms-dev.github.io/)
- [Sharif-Judge](https://github.com/mjnaderi/Sharif-Judge)
- [DMOJ](https://github.com/DMOJ/judge)
- [voj](https://github.com/hzxie/voj)
{: .list-normal }

##### আরও কিছু
- [What Every Programmer Should Know About Memory](https://www.akkadia.org/drepper/cpumemory.pdf)
- [Understanding Process memory](https://techtalk.intersec.com/2013/07/memory-part-2-understanding-process-memory/)
- [Memory Management](http://tldp.org/LDP/tlk/mm/memory.html)
- [Runtime Memory Measurement](https://elinux.org/Runtime_Memory_Measurement)
{: .list-normal }


#### **Refences**
---
 - Moe – Design of a Modular Grading System - Martin MAREŠ
 - Using a Linux Security Module for Contest Security - Bruce MERRY
 - Security of Programming Contest Systems - Michal Forišek
 - SECURITY SANDBOXING FOR PC 2 - Vikram Chidanand Adithya
{: .reference-list }


#### শেষের আগে
---
ব্যক্তিগত কৌতূহল থেকে এবং পরবর্তীতে একাডেমিক প্রোজেক্ট এর অংশ হিসেবে ভার্সিটির জন্য অনলাইন জাজ ডেভেলপমেন্ট শুরু করি। সেই  ডেভেলপমেন্ট এর ক্ষুদ্র অভিজ্ঞতা থেকেই এই লেখাটা। আমার ক্ষুদ্র প্রচেষ্টাটি আপাতত ওপেনসোর্স হিসেবে [গিটহাবেই](http://justoj.org/) পাওয়া যাবে  :) .




<!-- <div class="ssk-group">
    <a href="" class="ssk ssk-facebook"></a>
    <a href="" class="ssk ssk-twitter"></a>
    <a href="" class="ssk ssk-google-plus"></a>
    <a href="" class="ssk ssk-pinterest"></a>
    <a href="" class="ssk ssk-tumblr"></a>
</div>
 -->


<!-- <script type="text/javascript" src="/js/social-share-kit.min.js"></script> -->
<script>
hljs.initHighlightingOnLoad();
//SocialShareKit.init();
</script>










