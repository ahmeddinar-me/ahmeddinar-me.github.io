---
layout: post
title:  "কম্পিউটারের আদ্যোপান্ত"
date:   2017-11-21 00:00:01
author: Ahmed Dinar
categories: Development
tags: cpu ram logic-gate half-adder flip-flop full-adder alu control-unit kernel os compiler machine-code
share: true
---
* content
{:toc}

![diagram](/img/how_computer_works.jpg){: width="90%" }
<!-- image source: https://www.bcg.com/publications/2016/double-game-of-digital-action-structuring-the-program.aspx -->

কম্পিউটার কিভাবে কাজ করে? ইলেক্ট্রিসিটি কিভাবে ইমেজ, অডিও, ভিডিও তে রূপান্তরিত হয়? র‍্যাম, প্রসেসর এর ভিতর আসলে কি থাকে? কম্পিউটার একটা প্রোগ্রামই বা রান করে কিভাবে? আমার ক্ষুদ্র জ্ঞান এবং পাহাড় সমান কৌতূহল নিয়ে লিখতে বসা!




#### **ইলেকট্রিসিটি, ট্রান্সিস্টর এবং ক্যাপাসিটর**
---
আমরা স্কুল/কলেজেই পড়ে এসেছি ইলেকট্রিসিটি হল ইলেক্ট্রনের প্রবাহ বা ফ্লো। এই ফ্লো কে নিয়ন্ত্রণের জন্য তৈরি করা হয়েছে ট্রান্সিস্টরের। **ট্রান্সিস্টর** হল এক ধরনের ইলেকট্রনিক ডিভাইস যা সুইচ হিসেবে কাজ করে (কারেন্ট অন বা অফ করতে পারে)।

![diagram](/img/transistor.png){: width="300px" }
[image source](https://learn.sparkfun.com/tutorials/transistors){: style="font-size: 12px; text-align: center; margin: 0 auto; display: block;" }
<!--  -->

**ক্যাপাসিটর** হল একধরনের বৈদ্যুতিক যন্ত্রাংশ যা ইলেকট্রিক চার্জ ধারণ বা সংরক্ষন করে রাখতে পারে। এটাকে রিচার্জেবল ব্যাটারির সাথে তুলনা করা গেলেও, এটা খুবি ক্ষুদ্র পরিমান চার্জ ধারন করতে পারে। এই ট্রান্সিস্টর এবং ক্যাপাসিটর হল কম্পিউটারের ক্ষুদ্রতম অংশ। এগুলো ব্যবহার করে তৈরি করা হয় র‍্যাম, প্রসেসর ইত্যাদি। ট্রান্সিস্টর কিভাবে কাজ করে, কিভাবে বানানো হয়, n-p-n, p-n-p ইত্যাদি ইত্যাদি আমরা পড়ে এসেছি বা পড়ব, বিস্তারিত লিখতে গেলে অনেক বড় হয়ে যাবে!

#### **বিট, বাইট এবং মেমোরি (র‍্যাম)**
---
##### **বিট**
একটা কথা অনেক সময়ই শুনে থাকি "কম্পিউটার শুধু শূন্য এবং এক ব্যতিত আর কিছু বুঝেনা" অথবা "কম্পিউটারে সবকিছু শূন্য আর এক হিসেবে থাকে"। এই শুন্য অথবা এক ই হল বিট বা বাইনারি ডিজিট। বিট হল কম্পিউটারের তথ্যের ক্ষুদ্রতম একক। এই একটা বিট (শুন্য বা এক) কিভাবে ইলেকট্রিসিটি থেকে পাওয়া যায়? ব্যপারটা এই ভাবে চিন্তা করা যায়: **কারেন্ট থাকলে ১, না থাকলে ০** অথবা **হাই ভোল্টেজ ১, লো ভোল্টেজ ০**। কম্পিউটারে ট্রান্সিস্টর এবং ক্যাপাসিটর ব্যবহার করে কারেন্ট কে নিয়ন্ত্রণ এবং সংরক্ষন করে ০ এবং ১ হিসেবে ব্যবহার করা হয়। *ক্যাপাসিটরের ক্ষেত্রে এভাবে ধরা যায় "চার্জ থাকলে ১ , না থাকলে ০"*। *ট্রান্সিস্টরের ক্ষেত্রে "অন থাকলে বা কারেন্ট প্রবাহ হলে ১, না হলে ০"*। উপরের ব্যাখ্যাটি ০ এবং ১ বোঝার জন্য সহজ। কিন্তু আসলে শুধুমাত্র একটা বিট সংরক্ষন করার জন্য একাধিক ট্রান্সিস্টর অথবা ট্রান্সিস্টর এবং ক্যাপাসিটর একসাথে ব্যবহার করা হয়।

##### **বাইট**

আটটি বিটকে একত্রে **বাইট** বলা হয়। যেমনঃ 10010101, 00000000, ইত্যাদি। এই বাইট এর মাধ্যমে কম্পিউটারে অক্ষর (A-Z, a-z), সংখ্যা (0-9) এবং অন্যান্য চিহ্ন(+-=?"" ইত্যাদি) প্রকাশ করা হয়। কোন ক্যারেক্টারের কোন বাইট তা আগে থেকেই নির্ধারণ করা আছে। **[এই লিংকে ASCII টেবিলটিতে](http://www.rapidtables.com/code/text/ascii-table.htm)** একটু ঢু মেরে আসলেই দেখতে পাব 'A' কে প্রকাশ করা হয় 01000001 দিয়ে, 9 কে প্রকাশ করা হয় 00111001 দিয়ে, ইত্যাদি।

এখন **ধরি** যে একটা ক্যাপাসিটর একটা বিট সংরক্ষন করে। তাহলে পাশাপাশি আটটা ক্যাপাসিটর রাখলে হবে একটা বাইট! এখন যদি 'A'(01000001) সংরক্ষন করতে হয় আটটা পাশাপাশি ক্যাপাসিটরে, তাহলে বাম পাশ থেকে দ্বিতীয় এবং অষ্টম ক্যাপাসিটরে চার্জ থাকবে, বাকি গুলোতে চার্জ থাকবেনা!

###### **কেন ১ বাইট = ৮ বিট?**

আমরা যদি ASCII টেবিলটি খেয়াল করি, দেখব সর্বমোট ক্যারেক্টার আছে ২৫৬ টি (০ থেকে ২৫৫)। কম্পিউটারের বিট হল দুইটা(০,১), তাহলে ৮ টা বিট দিয়ে টোটাল ২^৮ = ২৫৬ টি ভিন্ন ক্যারেক্টার প্রকাশ করা যায়। তাই ACII(American Standard Code for Information Interchange) স্ট্যান্ডার্ড ক্যারেক্টার গুলোর জন্য ৮ টি বিটই যথেষ্ট। এটা স্ট্যান্ডার্ড হলেও প্রথম দিক শুরু হয়েছিল ৫ বিট দিয়ে। এরপর আরও ক্যারেক্টার সাপোর্ট এর জন্য বিট বাড়ানো হয়।
আরও জানতেঃ

[WIKI](https://en.wikipedia.org/wiki/Byte) ,
[Why is a byte EXACTLY 8 bits](https://www.quora.com/Why-is-a-byte-EXACTLY-8-bits)
এবং
[History of why bytes are eight bits?](https://softwareengineering.stackexchange.com/questions/120126/what-is-the-history-of-why-bytes-are-eight-bits)

##### **র‍্যাম**

কম্পিউটার মেমোরি হল অনেকগুলো মেমোরি সেল [(Memory Cell)](https://en.wikipedia.org/wiki/Random-access_memory#Memory_cell) এর সমন্বয়। মেমোরি সেল হল ইলেক্ট্রনিক সার্কিট যা একটা বিট সংরক্ষন করে। তারমানে, মেমোরি হল অনেকগুলো ০ আর ১ এর সমন্বয়। বিট এর উদাহরনে ধরেছিলাম একটা ক্যাপাসিটর একটা বিট সংরক্ষন করে, কিন্তু বাস্তবে কয়েকটা ট্রান্সিস্টর আর ক্যাপাসিটর দিয়ে সার্কিট বানানো হয় যা একটা বিট সংরক্ষন করে। কয়টা ব্যবহার করা হয় টা র‍্যাম ভেদে ভিন্য হয়। র‍্যাম [(RAM - Random access memory)](https://en.wikipedia.org/wiki/Random-access_memory) হল কম্পিউটারের প্রাথমিক মেমোরি।

**SRAM (Static RAM)** এ শুধু ট্রান্সিস্টর ব্যবহার করা হয় একটা বিট সংরক্ষনের জন্য। এর জন্য ব্যবহার করা হয় ফ্লিপ-ফ্লপ [(Flip Flop)](https://en.wikipedia.org/wiki/Flip-flop_%28electronics%29) সার্কিট যা ৬ টা ট্রান্সিস্টরের সমন্বয়ে গঠিত।

**DRAM (Dynamic RAM)** এ একটা ট্রান্সিস্টর এবং একটা ক্যাপাসিটর ব্যবহার করে মেমোরি সেল সার্কিট তৈরি করা হয়। তবে ক্যাপাসিটরে চার্জ লিক হয় বলে একটু পর পর মেমোরি রিফ্রেশ [(Memory refresh)](https://en.wikipedia.org/wiki/Memory_refresh) করা হয় যেন চার্জ হারিয়ে না যায়। এই জন্য একে Dynamic বলা হয়। Static RAM এ কোন রিফ্রেশ দরকার পরেনা।

![diagram](/img/ram_cells.jpg){: width="600px" }

**তাহলে ১ বাইট যদি ৮ বিট হয়, 1GB SRAM এ ট্রান্সিস্টর লাগবে ৬ * ৮ * ১০^১২ বা ৪৮ বিলিয়ন! আর 1GB DRAM এ ট্রান্সিস্টর এবং ক্যাপাসিটর লাগবে ৮*10^12 বা ৮ বিলিয়ন করে!** আমাদের ল্যাপটপ অথবা কম্পিউটারে যে র‍্যাম ব্যবহার করি, তাতে প্রকৃতপক্ষেই বিলিয়ন ট্রান্সিস্টর থাকে। ন্যানো টেকনোলজি এর মাধ্যমে অতি ক্ষুদ্র ট্রান্সিস্টর তৈরি করা হয়। কতটা ক্ষুদ্র? নিচে আমরা সেটা দেখব। আমরা ডেক্সটপ, ল্যাপটপ এ যে র‍্যাম ব্যবহার করি তা DRAM (আসলে এখন DRAM এরই উন্নত ভার্সন [DDR SDRAM](https://en.wikipedia.org/wiki/Synchronous_dynamic_random-access_memory) ব্যবহার হয়)। SRAM ব্যবহার করা হয় cpu cache হিসেবে।

 - এক্সপ্লেনেশন ভিডিও - [RAM Explained - Random Access Memory](https://www.youtube.com/watch?v=PVad0c2cljo&t=2s)

#### **বুলিয়ান অ্যালজেবরা(Boolean Algebra) এবং লজিক গেইট (Logic Gate)**
---
ইংরেজ গনিতবিদ [George Boole](https://en.wikipedia.org/wiki/George_Boole) ১৮৪৭ সালে তার The Mathematical Analysis of Logic নামে বইটিতে প্রথম বুলিয়ান অ্যালজেবরার উপস্থাপন করেন। এই অ্যালজেবরায় ভেরিয়েবল এর মান হবে দুইটি। true এবং false। এই true এবং false কে যথাক্রমে ১ এবং ০ দ্বারা প্রকাশ করা হয়। আজকের ডিজিটাল ইলেক্ট্রনিক্স এবং ইলেক্ট্রিক কম্পিউটার এর মুল ভিত্তি হল এই বুলিয়ান অ্যালজেবরা। নিচের ছবিটিতে বুল‌িয়ান অ্যালজ‌েবরার বেসিক গাণ‌িতিক অপরে‌শনগুল‌ো দেখানো হয়েছে। এখানে ^,∨ এবং ¬ কে যথাক্রমে AND, OR এবং NOT বলা হয়।

![diagram](/img/booleanalg.PNG){: width="200px" }

১৯৩৭ সালে গনিতবিদ [Claude Shannon](https://en.wikipedia.org/wiki/Claude_Shannon) প্রথম বুলিয়ান অ্যালজেবরা ব্যবহার করে ইলেক্ট্রনিক রিলে এবং সুইচের ডিজাইন বের করেন যা আসলে আজকের ডিজিটাল সার্কিটের শুরু।

[লজিক গেইট](https://en.wikipedia.org/wiki/Logic_gate) হল ইলেকট্রনিক সার্কিট যার মাধ্যমে বুল‌িয়ান অ্যালজ‌েবরার এই গাণ‌িতিক অপরে‌শনগুল‌োকে প্রয়োগ করা হয়। লজিক গেটে একাধিক ইনপুট থাকে আর আউটপুট থাকে একটি। নিচের টেবিলটিতে বিভিন্ন লজিক গেট এর সিম্বল আর গাণ‌িতিক অপরে‌শন দেখা যাচ্ছে।

![diagram](/img/logic_gates.jpg){: width="650px" }
[image source](https://imgur.com/){: style="font-size: 12px; text-align: center; margin: 0 auto; display: block;" }

এখানে AND গেট এর truth table টি ব্যাখ্যা দেখি। A এবং B হল দুইটি ইনপুট এবং X হল আউটপুট। যখন A আর B দুইটিই 1 তখন আউটপুট 1, বাকি যেকোন ইনপুট এর জন্য 0। বাস্তবে এই 1 এবং 0 হল কারেন্ট বা ভোল্টেজ। তারমানে AND গেটে যদি দুইটি ইনপুটেই কারেন্ট দেওয়া হয়, তাহলেই কেবল আউটপুটে কারেন্ট পাওয়া যাবে। বাকি সব গুলো গেট  ঠিক এভাবেই কাজ করে।

এখন প্রশ্ন হল কিভাবে গেট তৈরি করা হয়? **লজিক গেট আসলে কতগুলো ট্রান্সিস্টর দিয়ে তৈরি একটা সার্কিট।** নিচের ছবিটি তে দুইটি ট্রান্সিস্টর দিয়ে কিভাবে একটা AND গেট তৈরি হয় তার সার্কিট দেখানো হয়েছে।

![diagram](/img/TransistorANDgate.png){: width="150px" }

আরও বিভিন্ন লজিক গেট টেকনোলজি জানতেঃ [Logic Family](https://en.wikipedia.org/wiki/Logic_family) .

###### **Half Adder এবং Full Adder**

খুব ছোট একটা উদাহরণ দেখা যাক এই লজিক গেট এর বাস্তব প্রয়োগের। আমরা যদি বাইনারি অপারেশন বুঝে থাকি তাহলে আমরা নিচের ছবিটির বাইনারি যোগের truth table টি জানি।

![diagram](/img/half_adder.PNG){: width="350px" }
![diagram](/img/halfadderanimation.gif){: width="400px" }
[image source](http://www.electronics-tutorials.ws/combination/comb_7.html){: style="font-size: 12px; text-align: center; margin: 0 auto; display: block;" }

<!-- Image: http://electronicsgurukulam.blogspot.com/2012/05/half-adder-animation.html -->


বাম পাশের Symbol এ দেখানো হয়েছে কিভাবে একটা XOR এবং একটা AND গেট দিয়ে দুইটি বিট এর যোগফল এবং carry পাওয়া যায়। carry কি? আমরা যদি স্বাভাবিক ভাবে 6 এবং 7 কে যোগ করি, তাহলে যোগফল আসে 13, যার 3 আমরা লিখি এবং বলি "হাতে থাকে 1" এবং আরও ডিজিট থাকলে এই 1 টি তার সাথে যোগ হয়। এই বাইনারির নিয়মে তেমনি 1 + 1 = 10, তাই 0 লিখে হাতে থাকে বা carry থাকে 1। উপরের এই সার্কিট টির নাম [Half Adder](https://en.wikipedia.org/wiki/Adder_(electronics)#Half_adder)। কারন এখানে পূর্ববর্তী যদি কোন carry থাকে, তা আগে যোগ করে নেওয়ার সুযোগ নেই। যে সার্কিটে এই সুযোগ টি আছে তাকে বলা হয় [Full Adder](https://en.wikipedia.org/wiki/Adder_(electronics)#Full_adder)। নিচের ছবিটি Full Adder যা পূর্ববর্তী carry Cin হিসেবে নেয়।

![diagram](/img/full_adder.jpg){: width="600px" }

কয়েকটি Full Adder মিলে তৈরি হয় **[Adder](https://en.wikipedia.org/wiki/Adder_(electronics))** যা একাধিক বিট এর যোগফল নির্ণয় করে। Adder এর মত কয়েকটা Full Subtractor মিলে তৈরি হয় একটা [Subtractor](https://en.wikipedia.org/wiki/Subtractor) যা বিয়োগফল নির্ণয় করে।

চমৎকার এক্সপ্লেনেশন ভিডিও: [Digital Electronics: The Half Adder and Full Adder](https://www.youtube.com/watch?v=mZ9VWA4cTbE)

###### **Flip-Flop সার্কিট**

Flip-Flop সার্কিট একটা বিট সংরক্ষণের জন্য ব্যবহার করা হয়। একটা Flip-Flop সার্কিট একটা মেমরি সেল হিসেবে কাজ করে। এই সার্কিটে অনবরত কারেন্ট পাস করা হয় এবং একটি সেট এবং রিসেট ইনপুট থাকে। সেট ইনপুট আউটপুট বিট ১ করে এবং রিসেট অউটপুট বিট ০ করে। তারমানে অনবরত কারেন্ট থেকে এই সার্কিটের মাধ্যমে ০ বা ১ পাওয়া যায় যাকে আমরা বিট সংরক্ষণ বা সেভ বলে থাকি।

আমরা আগেই জেনেছি SRAM এ এই সার্কিট ব্যবহৃত হয়। এছাড়া প্রসেসর এর রেজিস্টরে ব্যবহৃত হয়। এই সার্কিট থেকে একটা ধারনা পেতে পারি কেন পাওয়ার অফ করলে র‍্যামের তথ্য হারিয়ে যায়। এই জন্য র‍্যামকে বলা হয় volatile memory (যদিও DRAM এর ক্ষেত্রে ক্যপাসিটর চার্জ হারায়). নিচের ছবি দুইটিতে আসলে দেখা যাচ্ছে latch. কয়েকটা latch মিলে তৈরি হয় একটা ফ্লিপ-ফ্লপ। ফ্লিপ-ফ্লপে সেট এবং রিসেট বাদেও আরও একটা ইনপুট থাকে যাকে বলা হয় clock ইনপুট।

![diagram](/img/flipflopset.gif){: width="250px" style="margin-right: 25px;" }
![diagram](/img/flipflopreset.gif){: width="250px" }
[image source](http://electronicsgurukulam.blogspot.com/2012/07/sr-flip-flop-animation.html){: style="font-size: 12px; text-align: center; margin: 0 auto; display: block;" }

 - চমৎকার এক্সপ্লেনেশন ভিডিওঃ [Latches and Flip-Flops 1 - The SR Latch](https://www.youtube.com/watch?v=-aQH0ybMd3U)
 - বিভিন্ন ফ্লিপ-ফ্লপ সম্পর্কেঃ [Know all about Latches and Flip Flops](https://www.edgefx.in/digital-electronics-latches-and-flip-flops/)

#### **প্রসেসর (Processor)**
---
প্রসেসর বা CPU (Central Processing Unit) কে বলা হয় কম্পিটারের ব্রেইন। প্রসেসর হল এক ধরনের ইলেক্ট্রনিক সার্কিট যা Instruction এর মাধ্যমে কম্পিউটারের সব অপারেশন নিয়ন্ত্রণ এবং সম্পাদন কর। একটা প্রসেসর এর প্রধান অংশ গুলো দেখি।

###### **Arithmetic Logic Unit (ALU)**

ALU একধরণের ইলেক্ট্রনিক সার্কিট যা গাণিতিক অপারেশন (যোগ, বিয়োগ ইত্যাদি) গুলো করে থাকে। ALU তৈরি করা হয় অনেকগুলো লজিক গেট এর মাধ্যমে। আমরা Adder এবং Subtractor সম্পর্কে জেনেছি, এই দুইটি ALU এর অংশ যার মাধ্যমে ALU যোগ, বিয়োগ করে থাকে। এখন প্রশ্ন হতে পারে কিভাবে গুন এবং ভাগ করে থাকে? Adder ব্যবহার করেই গুন এবং ভাগ এর কাজ করা হয়। এছাড়া [Floating Point Unit বা FPU](https://en.wikipedia.org/wiki/Floating-point_unit) ভগ্নাংশ হিসাবের কাজ করে থাকে. [Wiki - Binary Multiplier](https://en.wikipedia.org/wiki/Binary_multiplier) .

 - দারুন একটা আর্টিকেলঃ [Computer Arithmetic](https://www.cise.ufl.edu/~mssz/CompOrg/CDA-arith.html)
 - [how do computers multiply numbers together?](https://www.reddit.com/r/askscience/comments/25agig/at_the_hardware_level_how_do_computers_multiply/)
 - [How does division occur in our computers?](https://electronics.stackexchange.com/a/22445)
 - চমৎকার এক্সপ্লেনেশন ভিডিওঃ [How Computers Calculate - the ALU](https://www.youtube.com/watch?v=1I5ZMmrOfnA)

###### **Control Unit (CU)**

Control Unit প্রসেসর এর অপারেশন নিয়ন্ত্রন করে। কম্পিটার মেমরি, ALU, বিভিন্ন সংযুক্ত ডিভাইচ কিভাবে একটা Instruction অনুযায়ী কাজ করবে তা বলে দেয় এই কন্ট্রোল ইউনিট।

###### **Register**

[Processor Register](https://en.wikipedia.org/wiki/Processor_register) প্রসেসরে সাময়িকভাবে ডাটা সংরক্ষণের জন্য ব্যবহার করা হয়। আমরা Flip-Flop সম্পর্কে জেনেছি, এটি ব্যবহার করে Register তৈরি করা হয়। Register খুব অল্প পরিমান (মাত্র কয়েকটি বিট) মেমরি সংরক্ষন করে। যেমন ৪ বিট এর একটি Register এ পাশাপাশি ৪ টি Flip-Flop ব্যবহার করা হয়।

###### **CPU cache**

[CPU cache](https://en.wikipedia.org/wiki/CPU_cache) হল একধরনের মেমরি যা প্রসেসর এবং র‍্যাম এর মধ্যবর্তী সাময়িক মেমরি হিসেবে কাজ করে। র‍্যাম থেকে ডাটা আদান-প্রদান এর স্পিড বৃদ্ধি করার জন্য cache ব্যবহার করা হয়।

###### **Moore's law**

Moore's law হল ট্রান্সিস্টর এর সাইজ বা আইসি তে এর সংখ্যা নিয়ে একটা ভবিষ্যদ্বাণী যা Intel এর কো-ফাউন্ডার Gordon Moore এর নামানুসারে। এটি হল **আইসি (IC) তে ট্রান্সিস্টর এর সংখ্যা প্রতি দুই বছর পর পর দিগুন হবে।**। তারমানে, ট্রান্সিস্টর আরো ক্ষুদ্র হবে। এবং গত কয়েকযুগ ধরে এই ভবিষ্যদ্বাণী সত্য হয়ে আসছে।

![diagram](/img/inteltrasistor.jpeg){:width="500px"}

Intel ২০১২ সালে 3-D transistors তৈরি শুরু করে যার সাইজ ২২ ন্যনোমিটার (22nm)। বর্তমানে ব্যবহার করা হচ্ছে 14nm ট্রান্সিস্টর। Intel ২০১৭ অথবা ২০১৮ সাল নাগাদ 10nm ট্রান্সিস্টর আনবে। এই 22nm আসলে কতটা ক্ষুদ্র? নিচের লিংক গুলোতে একবার ঢুঁ মেরে আসলেই সেটা জানা যাবে।

- [Exactly how small (and cool) is 22 Nanometers?](https://www.intel.com/content/dam/www/public/us/en/documents/corporate-information/history-moores-law-fun-facts-factsheet.pdf)
- [Mark Bohr Gets Small: 22nm Explained- Intel](https://www.youtube.com/watch?v=YIkMaQJSyP8)
- [The Making of a Chip with 22nm/3D Transistors](https://www.youtube.com/watch?v=d9SWNLZvA8g)
- [14 nm Transistor Explained](https://www.intel.com/content/www/us/en/silicon-innovations/standards-14nm-explained-video.html)

বিভিন্ন প্রসেসরে কত গুলো ট্রান্সিস্টর থাকে তার একটা লিস্ট এই লিঙ্ক এ পাওয়া যাবে।
- [Transistor Count - WIKI](https://en.m.wikipedia.org/wiki/Transistor_count)

#### **প্রসেসর কিভাবে কাজ করে?**
---
প্রসেসর শুধু Instruction বুঝে এবং সেই অনুযায়ী কাজ করে। এই Instruction হতে পারে র‍্যাম থেকে কোন ডাটা রিড করা অথবা রাইট করা, যোগবিয়োগ করা ইত্যাদি। এই Instruction থাকে বাইনারি ডিজিট হিসেবে। যেমন ধরি ADD = 1000। তারমানে প্রসেসর কে Instruction হিসেবে 1000 দিলে প্রসেসর বুঝবে যে এখন ADD বা যোগ করতে হবে। প্রতিটা CPU এর কোন Instruction এর জন্য কোন বাইনারি তা নির্ধারণ করা থাকে। [এই লিংকে Intel 4004 CPU (Intel এর প্রথম CPU যা ছিল মাত্র ৪ বিট এর) এর Instructions Set পাওয়া যাবে।](http://e4004.szyc.org/iset.html) .

কম্পিউটারে সিপিইউ, র‍্যাম ইত্যাদি আলাদা অংশের ভিতর সংযোগ স্থাপনের জন্য এক ধরনের বিদ্যুৎ পরিবাহী লাইন (Wire) ব্যবহার করা হয়, যাকে বলা হয় [Bus](https://en.wikipedia.org/wiki/Bus_(computing)) এবং সিপিইউ এর সাথে যে বাসের মাধ্যমে অন্যান্য অংশ যুক্ত থাকে তাকে বলা হয় [System Bus](https://en.wikipedia.org/wiki/System_bus) ।

![computer_system_bus](/img/computer_system_bus.png){: width="200px" }

আমরা আগেই দেখেছি র‍্যাম বা মেমরি হল অনেক গুলো ০ আর ১ এর সমষ্টি। এখন এই র‍্যামে কোন ডাটা কোথায় আছে তা নির্ধারণের জন্য [Memory Address](https://en.wikipedia.org/wiki/Memory_address) ব্যবহার করা হয়। একে অনেকটা বইয়ের পেজ নাম্বারের সাথে তুলনা করা যায়। এই Memory Address ও হল বাইনারি ডিজিট। নিচের ছবিতে বাম পাশের Hexadecimal সংখ্যা গুলো Memory Addres।

![memory_adress](/img/memory_adress.gif){: width="180px" }

মেমরি থেকে কোন ডাটা রিড করতে অথবা সেভ করতে Memory Address এর দরকার হবে। কোন Address এ ডাটা যাবে অথবা আসবে তা যে রেজিস্টরে থাকে তাকে বলা হয় [Memory Address Register (MAR)](https://en.wikipedia.org/wiki/Memory_address_register)। আমরা জেনেছি যে রেজিস্টর কয়েক বিট সংরক্ষন করে। প্রতিটা বিট এর জন্য একটা করে সংযোগ তার থাকে। তেমনি ৮ বিট এর রেজিস্টরে সংযোগের জন্য ৮ টা তার থাকবে, এবং এই তার গুলোকে আমরা জানি বাস (Bus) নামে। যে বাস এর সাহায্যে Address Register যুক্ত তাকে বলা হয় [Address Bus](https://en.wikipedia.org/wiki/Address_bus)। আবার ডাটা গুলোও বাইনারি বিট এবং এই ডাটা যে বাস এর মাধ্যমে যায় তাকে বলা হয় Data Bus। প্রসেসর কোন ডাটা মেমোরি তে পাঠাবে অথবা কোন ডাটা মেমরি থেকে রিড করল তা সংরক্ষণের জন্য ব্যবহার করে [Memory Data Register(MDR)](https://en.wikipedia.org/wiki/Memory_data_register) যেটা Memory Buffer Register (MBR) নামেও পরিচিত।

![memory_adress](/img/systm_buses.gif){: width="400px" }

প্রসেসর অনেকগুলো Instruction ক্রমান্বয়ে সম্পন্ন করে, একটি সম্পন্ন হলে আরেকটি শুরু করে। [Program Counter বা PC](https://en.wikipedia.org/wiki/Program_counter) হল একধরনের Register যা পরবর্তী Instruction কি হবে তা সেভ করে রাখে। একটি Instruction এর কাজ শুরু হলে এই PC এর মান পরবর্তী Instruction কোন Memory Adress এ আছে তা সেভ করে। [Instruction Register (IR)](https://en.wikipedia.org/wiki/Instruction_register) বর্তমানে যে Instruction এর কাজ চলছে তা সংরক্ষন করে।

প্রসেসর Instruction প্রসেস করার জন্য প্রধানত তিনটি ধাপে করে।

**১. Fetch instruction** ধাপে প্রসেসর Program Counter থেকে Memory Adress নিয়ে MAR এ পাঠায় এবং Address Bus এর মাধ্যমে র‍্যাম থেকে instruction টি MDR এ রিড করে রাখে। এরপর MDR থেকে instruction টি Instruction Register এ পাঠায় সেটার কাজ শুরু করার জন্য।

**২. Decode instruction** ধাপে প্রসেসর Instruction Register এ থাকা instruction টি decode করে বা instruction দ্বারা আসলে কি করতে বলা হয়েছে তার সিদ্ধান্ত নেয়। এই কাজটি প্রসেসর এর Control Unit করে থাকে।

**৩. Execute instruction** ধাপে প্রসেসর Instruction অনুযায়ী কাজ করে। কোন গাণিতিক হিসাব করার থাকলে ALU এর মাধ্যমে তা সম্পাদন করে। ALU এর ভিতর [Accumulator Register](https://en.wikipedia.org/wiki/Accumulator_(computing)) নামক রেজিস্টর থাকে যা গাণিতিক হিসাব এবং এর ফলাফল সংরক্ষণের জন্য ব্যবহার করা হয়। এই ধাপ শেষে ফলাফল আবার মেমরি তে পাঠায় অথবা কোন আউটপুট ডিভাইচে পাঠায়।

![fetch_execute_slow](/img/fetch_execute_slow.gif){: width="400px" }
[image source](https://www.doc.ic.ac.uk/~eedwards/compsys/cpu/){: style="font-size: 12px; text-align: center; margin: 0 auto; display: block;" }

এই সবগুলো ধাপকে বলা হয় [Instruction Cycle](https://en.wikipedia.org/wiki/Instruction_cycle)। প্রতি সেকেন্ডে 1 Cycle কে বলা হয় Hertz। তারমানে 1 Hertz হল 1 সেকেন্ডে 1 টি Cycle। 1 megahertz(MHz) হল 1 সেকেন্ডে 1,000,000 টি Cycle এবং 1 gigahertz (GHz) হল 1 সেকেন্ড 1,000,000,000 টি Cycle। তারমানে আমাদের প্রসেসর স্পিড যদি হয় 2GHz, তাহলে এটি মাত্র ১ সেকেন্ডে 1,000,000,000 টি Instruction সম্পন্ন করতে পারে! এর থেকে প্রসেসর স্পিড সম্পর্কে ধারনা পাওয়া যায়। তবে একটা প্রসেসর এর পারফরমেন্স আরও কিছু বিষয়ের উপর নির্ভর করে। আরও জানতেঃ [Instructions per second (IPS)](https://en.wikipedia.org/wiki/Instructions_per_second) এবং [Instruction per cycle (IPC)](https://en.wikipedia.org/wiki/Instructions_per_cycle)।

![fetch-execute-cycle](/img/fetch-execute-cycle.png){: width="300px" }
[image source]( https://jackcarr0.wordpress.com/2014/03/10/the-fetch-decode-execute-cycle/){: style="font-size: 12px; text-align: center; margin: 0 auto; display: block;" }

 - চমৎকার ভিডিও - [Fetch Decode Execute Cycle in more detail](https://www.youtube.com/watch?v=jFDMZpkUWCw)

#### **প্রোগ্রামিং ল্যাঙ্গুয়েজ, মেশিন ল্যাঙ্গুয়েজ এবং কম্পাইলার। প্রসেসর কিভাবে প্রোগ্রাম রান করে?**
---

ধরি মেমরির 75 নাম্বার এড্রেস এ 6 আছে এবং 76 নাম্বার এড্রেস এ 7 আছে (বোঝার সুবিধার্থে বাইনারি ব্যবহার না করে ডেসিমাল ব্যবহার করি)। এখন এই 6 এবং 7 এর যোগফল বের করতে হলে  Instruction কিভাবে হবে? ধরি A এবং B প্রসেসর এর দুটি Register।

{% highlight cpp %}
MOV 75, A
MOV 76, B
ADD A, B
MOV A, 77
{% endhighlight %}

এখানে ``MOV 75 A`` একটি Instruction যা নির্দেশ করে 75 মেমরি এড্রেস থেকে ডাটাটি A নামক Register এ রাখ (A = 6)। তেমনি ``MOV 76 B`` নির্দেশ করে 76 মেমরি এড্রেস থেকে ডাটাটি B নামক Register এ রাখতে (B = 7)। ``ADD A, B`` নির্দেশ করে A এবং B Register এর মান যোগ করে A Register এ রাখত (A = 13)। সর্বশেষ ``MOV A 77`` Instruction টি নির্দেশ করে A Register এ থাকা যোগফল 77 নাম্বার এড্রেস এ সেভ করতে। এখানে অবশ্যই ``MOV`` এবং ``ADD``, এড্রেস সবকিছু প্রসেসরে বাইনারি হিসেবে যাবে এবং প্রসেসর Decode করে বুঝতে পারবে আসলে উপরের মত নির্দেশ গুলো দেওয়া হচ্ছে এবং তা সম্পন্ন করবে।

আরেকটা উদাহরণ দেখি। ``x = 5 + ( 7 – 3 ) * 2`` হিসাবটি যদি আমরা করতাম তাহলে কিভাবে করতাম? প্রথমে 7 এবং 3 এর বিয়োগ করতাম, তারপর বিয়োগফলের সাথে 2 গুন করতাম, সবশেষে 5 যোগ করে ফলাফল পেতাম। প্রসেসর অনেকটা এভাবেই কাজ করে। এই হিসাবটির জন্য Instruction কেমন হতে পারে দেখিঃ

{% highlight cpp %}
MOV A, 7
SUB A, 3
MUL A, 2
ADD A, 5
{% endhighlight %}

এখানে SUB = subtraction এবং MUL = multiplication হিসেবে লেখা। এখন এই ভেলু গুলো যদি র‍্যাম বা মেমরি তে থাকে, তাহলে সরাসরি যোগবিয়োগ না করে মেমরি অ্যাড্রেস থেকে ভেলুগুলো এনে তারপর হিসাব করতে হবে। ধরি x, 5 , 7 , 3 এবং 2 আছে যথাক্রমে 404, 407, 488, 209, 310 নাম্বার মেমরি অ্যাড্রেসে। তাহলে মেমরি অ্যাড্রেস দিয়ে হিসাবটি দ্বারায় ``@404 = @407 + ( @488 – @209 ) * @310``। এখানে '@' দ্বারা মেমরি অ্যাড্রেস বোঝানো হয়েছে। Instruction কেমন হতে পারে দেখিঃ

{% highlight cpp %}
MOV A, 488
MOV B, 209
SUB A, B
MOV B, 310
MUL A, B
MOV B, 407
ADD A, B
MOV 404, A
{% endhighlight %}

উপরের উদাহরণটি অনেকটা [Assembly language](https://en.wikipedia.org/wiki/Assembly_language) এর মত। Assembly language হল [Low level প্রোগ্রামিং ল্যাঙ্গুয়েজ](https://en.wikipedia.org/wiki/Low-level_programming_language) যা দ্বারা সরাসরি প্রসেসরের Register গুলো ব্যবহার করে Instruction দিতে হয় যা মেশিন কোড এর খুব কাছাকাছি। [Machine Code বা মেশিন ল্যাঙ্গুয়েজ](https://en.wikipedia.org/wiki/Machine_code) হল অনেকগুলো Instruction এর সমন্বয় যা প্রসেসর সরাসরি বুঝতে পারে এবং সম্পাদন করতে পারে। নিচের কোডটি Assembly এর ৩২ বিট রেজিস্টর এর কোডঃ

{% highlight cpp %}
mov eax, 45
{% endhighlight %}

এখানে ``eax`` হল 32 bit Accumulator register। এভাবে সরাসরি Register নিয়ে কোড লিখতে গেলে বেশ কঠিন হয়ে পড়ে এবং বড়ও হয়ে যায়। এই জন্য আমাদের বোঝার সুবিধার জন্য আরও অনেক প্রোগ্রামিং ল্যাঙ্গুয়েজ তৈরি হয়েছে। এই ল্যাঙ্গুয়েজ এর কোড আমরা আমাদের পরিচিত ভাষায় (English) লিখতে পারি। যেমন উপরের হিসাবটি C প্রোগ্রামিং এ এরকম হবেঃ

{% highlight cpp %}
int x, a = 5, b = 7, c = 3, d = 2;
x = a + ( b – c ) * d;
{% endhighlight %}

এই কোড যেহেতু কম্পিউটার বুঝবেনা তাই [কম্পাইলার](https://en.wikipedia.org/wiki/Compiler) ব্যবহার করা হয় যা এই হাই লেভেল প্রোগ্রামিং ল্যাঙ্গুয়েজ এ লেখা কোড উপরের মত মেশিন Instruction এ রূপান্তরিত করে। আগের অনেক কম্পাইলার হাই লেভেল ল্যাঙ্গুয়েজ থেকে Assembly কোডে রূপান্তরিত করত। এখন অনেক মডার্ন কম্পাইলার গুলো সরাসরি মেশিন কোড জেনারেট করে।

আমরা যারা C প্রোগ্রামিং এবং পয়েন্টার নিয়ে জানি, কোন একটা ভেরিএবল ডিক্লেয়ার করলে তার একটা মেমরি এড্রেস থাকে। নিচের কোডটি রান করলে আমরা a এর জন্য একটা মেমরি এড্রেস দেখতে পাবো ``address of a = 0060FF0C``.

{% highlight cpp %}
int a;
a = 7;
printf("address of a = %p\n", (void*)(&a));
{% endhighlight %}

এখানে ``0060FF0C`` Hexadecimal নাম্বার যা ``a`` ভেরিএবল এর জন্য নির্ধারিত মেমরি অ্যাড্রেস। C কোড কম্পাইল করার পর উইন্ডোজে .exe ফাইল তৈরি হয় যাকে বলা হয় [Binary File](https://en.wikipedia.org/wiki/Binary_file)। এই ফাইল আমরা কোন একটা hexadecimal editor (যেমন [hxd](https://mh-nexus.de/en/hxd)) দিয়ে ওপেন করলে নিচের মত দেখাবেঃ

![hexa](/img/hexaeditor.PNG){: width="300px" }

অনেক গুলো hexadecimal ছাড়া আর কিছু নয়। কম্পাইলার আমাদের কোড কে অনেক গুলো বাইনারি নাম্বারের Instruction জেনারেট করে ফাইল তৈরি করে যা এডিটর hexadecimal হিসেবে দেখায়। মজার ব্যাপার হল আমরা এই এডিটর গুলো ব্যবহার করে আমাদের কম্পাইলড exe ফাইল পরিবর্তন করে অউটপুট পরিবর্তন করে ফেলতে পারি! [এই ভিডিও](https://www.youtube.com/watch?v=BTGEI_ZLbEc) তে পাওয়া যাবে।

 - [How processor, assembler, and programming languages work](https://www.codeproject.com/Articles/315505/How-processor-assembler-and-programming-languages)
 - [Assembly Registers](https://www.tutorialspoint.com/assembly_programming/assembly_registers.htm)

#### **ROM এবং BIOS**
---
[ROM বা Read Only Memory](https://en.wikipedia.org/wiki/Read-only_memory) হল একধরনের [Non Volatile Memory](https://en.wikipedia.org/wiki/Non-volatile_memory) যা কম্পিউটার স্টার্ট আপ এর কাজ করে। রমে যে তথ্য থাকে তা পরিবর্তন করা যায় না বললেই চলে। কম্পিউটার তৈরি করার সময়ই এতে এর প্রয়োজনীয় তথ্য দিয়ে দেওয়া হয়। [BIOS বা Basic Input/Output System](https://en.wikipedia.org/wiki/BIOS) একধরনের Firmware যা রমের মধ্যে অবস্থান করে। যখন আমরা কম্পিঊটার অন করি, তখন এই BIOS সর্বপ্রথম রান হয়। এটি রান হয়ে প্রথমে [power-on self-test বা POST](power-on self-test (POST)) প্রসেস রান করে। এই POST আসলে কিছু জিনিস টেস্ট করে নেয়, যেমন প্রসেসর registers চেক করা, র‍্যাম কানেক্ট আছে কিনা, র‍্যাম এর সাইজ কত চেক করা, বিভিন্ন কানেক্তেড ডিভাইচ চেক করা ইত্যাদি। কম্পিউটার স্টার্ট এর সময় নিচের মত কাল স্ক্রিনে অনেক সময় দেখতে পাই, যা POST এর অংশ।

![hexa](/img/POST2.png){: width="400px" }

POST টেস্ট শেষ হওয়ার পর সব ঠিক থাকলে BIOS এরপর MBR(Master Boot Record) এর মাধ্যমে হার্ডডিস্ক এর পার্টিশন চেক করে। এরপর বুট লোডার (যেমন [GRUB বা Grand Unified Bootloader](https://en.wikipedia.org/wiki/GNU_GRUB)) অপারেটিং সিস্টেম খুজে বের করে হার্ডওয়ারে, CD-ROM এ অথবা বুটেবল ডিভাইচে। পরবর্তীতে উপযুক্ত OS পেলে তার kernel কে রান করে। এটা হল একদম বেসিক কম্পিউটার স্টার্ট আপ। আরও জানতে [Booting](https://en.wikipedia.org/wiki/Booting).        

#### **Kernel এবং Operating System**
---
[Kernel](https://en.wikipedia.org/wiki/Kernel_(operating_system)) হল একটা অপারেটিং সিস্টেমের প্রধান অংশ। এটি একটা কম্পিউটার প্রোগ্রাম যা বুট লোডার এর পর প্রথম রান হয়। এটি অন্যান্য সব সফটওয়্যার এর প্রসেস রিকোয়েস্ট নিয়ন্ত্রন করে এবং বিভিন্ন ইনপুট/আউটপুট ডিভাইচ যেমন কিবোর্ড, মাউস, মনিটর,স্পিকার ইত্যাদিও নিয়ন্ত্রন করে। কম্পিউটারে যেকোন প্রোগ্রাম এর সাথে প্রসেসর এর সংযোগের সিদ্ধান্ত নেয় এই কার্নেল। এছাড়া সফটওয়্যার/প্রোগ্রাম কোন মেমরি ব্যবহার করবে, পর্যাপ্ত মেমরি আছে কিনা ইত্যাদি নিয়ন্ত্রন করে।

![Kernel_Layout](/img/Kernel_Layout.svg.png)

[Operating System](https://en.wikipedia.org/wiki/Operating_system) হল সিস্টেম সফটওয়্যার যা কম্পিউটার হার্ডওয়্যার এবং সফটওয়্যার রিসোর্স ব্যবহার কে নিয়ন্ত্রন করে। কম্পিউটার প্রোগ্রাম রান করতে হলে অপারেটিং সিস্টেমের দরকার হয় কেননা অপারেটিং সিস্টেমেই একটা কম্পিউটার প্রোগ্রাম কে সার্ভিস দিয়ে থাকে।

![OS](/img/165px-Operating_system_placement.svg.png)

#### **32-Bit, 64-Bit এবং র‍্যাম সাইজ**
---
আমরা ইতিমধ্যে জেনেছি যে মেইন মেমরি বা র‍্যাম এ মেমরি অ্যাড্রেস থাকে যার সাহায্যে প্রসেসর ডাটা এবং Instruction পায়। এই মেমরি অ্যাড্রেস যে রেজিস্টরে থাকে তাকে বলা হয় Adress Register. **এই Adress Register এর সাইজ এর উপর ভিত্তি করে প্রসেসর এর নামকরন হয়। 32 bit প্রসেসরে 32 bit Register থাকে, 64 প্রসেসরে 64 bit Register।** আমরা [Intel প্রসেসরের এই লিস্টে](https://en.wikipedia.org/wiki/List_of_Intel_microprocessors) একবার ঢুঁ মেরে আসলেই দেখতে পাব প্রথম প্রসেসর ছিল Intel 4004 যা ছিল 8 bit এর। 1978 সালে প্রথম 16 bit 8086 চিপ আনে। এরপর আসে 80386 , 80486। লাস্ট এ এই 86 এর কারনে এর নামকরন করা হয় x86 বা x86 architecture। এরপর যখন 64 bit প্রসেসর আনে তখন নামকরন করা হয় x86-64 বা x64।

একটা Adress Register যদি 2 bit হয়, তাহলে টোটাল ইউনিক অ্যাড্রেস হতে পারে 2^2 = 4 টি (00,01,10,11)। তাহলে 4 bit এর Adress Register এর জন্য 2^4 = 16 টি, এভাবে 32 bit এর জন্য হবে 2^32 = 4294967296 টি যা প্রায় 4 gigabyte(GB) এর সমান। তারমানে 32 bit সাইজ এর Adress Register এর চেয়ে বড় মেমরি অ্যাড্রেস সংরক্ষন করতে পারবে না। **এই কারনে 32 bit প্রসেসরে সর্বোচ্চ 4GB র‍্যাম ব্যবহার করা যায়।** আর 2^64 প্রায় 18-Billion GB!! বোঝাই যাচ্ছে 64 bit প্রসেসরে র‍্যাম এর সাইজ নিয়ে কোন লিমিট এখন পর্যন্ত নেই!

#### **হার্ডডিস্ক (HDD) | র‍্যাম কেন প্রয়োজন?**
---

হার্ড ডিস্ক হলো কম্পিউটারের আরেকটি মেমরি যা ডাটা সংরক্ষণ করে এবং পাওয়ার অফ করলেও ডাটা হারিয়ে যায়না। আমরা যে ফাইলগুলো 'সেভ' করে রাখি, কম্পিটারের বিভিন্ন সফটওয়্যার, এমনকি অপারেটিং সিস্টেম ও এই হার্ডডিস্ক সংরক্ষন করে। র‍্যাম বা Register এর মত এতে ট্রান্সিস্টর ব্যবহার না করে চৌম্বকীয় শক্তি ব্যবহার করে প্রতিটা বিট সংরক্ষন করা হয়। হার্ড ডিস্কে একাধিক চাকতি থাকে যেগুলো চৌম্বকীয় ধাতু দ্বারা আবৃত এবং এই চাকতি গুলো কে বলা হয় [প্লেটারস](https://en.wikipedia.org/wiki/Hard_disk_drive_platter)। এগুলোর সাথে আর্ম বা হাত থাকে থাকে যার ক্ষুদ্র মাথার সাহায্যে চৌম্বকীয় আবরণে বিট সেট এবং রিড করা হয়।

![hardDisk](/img/hdd.gif){: width="400px" }

র‍্যাম এ ডাটা রিড বা রাইট করা হার্ডডিস্ক থেকে অনেক দ্রুত হয়। [Solid-state drive বা SSD](https://en.wikipedia.org/wiki/Solid-state_drive) নামে নতুন আরেক ধরনের হার্ডডিস্ক আবিষ্কার হয়েছে যাতে র‍্যাম এর মত টেকনোলজি ব্যবহার করা হয়েছে যা HDD এর তুলনায় অনেক দ্রুত কাজ করতে পারে।  কম্পিটারে সব সফটওয়্যার এবং প্রোগ্রাম থাকে হার্ডডিস্কে। কোন একটা প্রোগ্রাম রান করলে প্রথমে হার্ডডিস্ক থেকে সেটা র‍্যাম এ লোড হয়, এরপর র‍্যাম থেকে প্রসেসর সেটি রান করে। যেমন আমরা একটা ছোট C এর প্রোগ্রাম লিখলে যে exe ফাইলটি তৈরি হয় তা আমাদের হার্ডডিস্কে থাকে। সেটি রান করলে তার ভিতর থাকা মেশিন কোডের Instruction গুলো র‍্যামে থাকে এবং প্রসেসর র‍্যাম থেকে নিয়ে সেগুলো এক্সিকিউট করে। যেহেতু র‍্যাম ক্ষণস্থায়ী, তাই ঐ প্রোগ্রাম এর কাজ শেষ হলে র‍্যাম থেকেও সেটা চলে যায়।

**সফটওয়্যার হল একাধিক কম্পিউটার প্রোগ্রাম এর সমষ্টি।** আর কম্পিউটার প্রোগ্রাম মানেই Instruction। যেমন আমরা যে ব্রাউজার ব্যবহার করি সেটিও একটি কম্পিউটার প্রোগ্রাম এর সমষ্টি যা আসলে অনেকগুলো Instruction ছাড়া আর কিছু না।

 - ভিডিও - [How a Hard Disk Drive Works](https://www.youtube.com/watch?v=NtPc0jI21i0)

#### **কিভাবে বাইনারি ডাটা ইমেজ, অডিও, ভিডিও তে রূপান্তরিত হয়?**
---
আমরা ইতিমধ্যে জানি যে কম্পিউটারে সব ডাটা 0 এবং 1 হিসেবে থাকে। আমরা যে সব ফাইল দেখি আমাদের কম্পিউটারে যেমন টেক্সট ফাইল, ইমেজ, অডিও, ভিডিও ইত্যাদি সবকিছু আসলে 0 এবং 1 ছাড়া আর কিছু নয়। মেমরির এই 0 এবং 1 কোনটি ইমেজ বা ভিডিও তা নির্ধারণ করে কম্পিটার প্রোগ্রাম, অর্থাৎ 0 এবং 1 কে কনভার্ট করে আমাদের সামনে মনিটরে ইমেজ, টেক্সট বা স্পিকারে সাইন্ড হিসেবে দেয় কিছু কম্পিটার প্রোগ্রাম। [**এই লিংকে এ সম্পর্কে আরও একটু বিস্তারিত পাওয়া যাবে**](https://www.quora.com/How-does-a-computer-program-convert-different-types-of-data-like-images-or-text-files-into-binary-data) এবং [BBC এর আর্টিকেল](https://www.bbc.co.uk/education/guides/zpfdwmn/revision/1)। এখানে শুধু সংক্ষেপে ধারণা দেওয়ার চেষ্টা করব।

###### **ইমেজ**

ইমেজ হল অনেকগুলো পিক্সেল এর সমষ্টি। পিক্সেল হল একটা ইমেজ এর ক্ষুদ্র অংশ। প্রতিটা পিক্সেল কিছু কালার থাকে এবং সবগুলো কালার মিলে আসল ইমেজটি পাওয়া যায়। নিচের বাম পাশের ছবিটিতে সবুজ বৃত্তের ভিতর সাদা তীর দেখা যাচ্ছে এবং কালো দাগে ছোট ছোট ঘর বা গ্রিড এ বিভক্ত। কিছ গ্রিড সাদা, কিছু গ্রিড সবুজ।

![OS](/img/image_pixel.gif){: width="200px" }
![OS](/img/image_pixels.png){: width="500px" }
[image source](http://www.datagenetics.com/blog/march12012/){: style="font-size: 12px; text-align: center; margin: 0 auto; display: block;" }


লাল(RED), সবুজ (GREEN) এবং নীল (BLUE) কে বলা হয় প্রাইমারি কালার। এই তিনটি কালার মিক্স করে আরও অনেক কালার বানানো যায় এবং এর নামকরন করা হয়েছে [RGB Color Model](https://en.wikipedia.org/wiki/RGB_color_model)। এই মডেল এ এই তিনটি কালার এর মান 0 থেকে 255 (টোটাল 256) হতে পারে। এই মডেলে এই তিনটি কালার ব্যবহার করে টোটাল 256x256x256 = 16777216 টি ভিন্ন কালার সম্ভব। ইমেজ এর জন্য প্রতিটা পিক্সেল যেহেতু আলাদা আলাদা কালার, প্রতিটাকে একটা RGB এর মাধ্যমে প্রকাশ করা যায়। একটা ইমেজ ফাইল বা ডাটা মেমরি তে প্রতিটা পিক্সেল এর এই মান গুলো শুধু সংরক্ষন করে রাখে।

 - ইন্টারেস্টিং! - [Why in RGB the biggest number for any particular color is 255?](https://www.quora.com/Why-in-RGB-the-biggest-number-for-any-particular-color-is-255) এবং [Why RGB is RGB!](https://www.quora.com/Why-do-computers-use-red-green-and-blue-instead-of-the-primary-colors)
 - [Color Depth](https://en.wikipedia.org/wiki/Color_depth) এবং [Image Compression](https://en.wikipedia.org/wiki/Image_compression)

###### **অডিও**

পদার্থ বিজ্ঞানে আমরা পড়ে এসেছি শব্দ হলো এক ধরনের তরঙ্গ বা Wave যা আমাদের কানে কম্পনের সৃষ্টি করে এবং আমরা শুনতে পাই। আমাদের কানে পর্দায় চাপ বা প্রেসার এর ফলে এই কম্পন সৃষ্টি হয়। এই Wave কে সময় আর প্রেসারে ভাগ করা যায়। তারমানে একটা নির্দিষ্ট সময়ে এই ওয়েভ কতটুকু প্রেসার সৃষ্টি করবে তার মান দিয়ে আমরা শব্দকে প্রেজেন্ট করতে পারি। একটা টাইম স্যাম্পল এর মাধ্যমে এই ভেলু গুলো বাইনারি হিসেবে মেমরি তে সংরক্ষন করা হয়। পরবর্তীতে এই ডাটা স্পিকারের সাহায্যে আবার Wave এ রুপান্তরিত করা হয়।

![soundwave](/img/soundwave.png){: width="300px" }
<!-- https://www.bbc.co.uk/education/guides/zpfdwmn/revision/3 -->

 - [Binary Representation of Sound](http://teachwithict.weebly.com/binary-representation-of-sound.html)
 - [How does a computer record and produce sound?](https://musicandcomputerscience.wordpress.com/how-does-a-computer-record-and-produce-sound/)

###### **ভিডিও**

ভিডিও হল মুভিং ইমেজ বা চলমান ছবি। আমাদের যদি [Flip Book](https://en.wikipedia.org/wiki/Flip_book) এর সাথে পরিচয় থাকে তাহলে ভিডিও এর একটা ধারনা এখান থেকে পাওয়া যায়। ফ্লিপবুক হল পর পর অনেক গুলো ছবি যার পরপর দুটি ছবির ভিতর সামান্য পার্থক্য থাকে এবং দ্রুত ছবিগুলো উল্টালে মনে হবে ছবিটি চলমান।  

![OS](/img/flipbook.gif)

ভিডিও তেমনি পর পর অনেক গুলো ইমেজ , যার প্রত্যেকটিকে বলা হয় [ফ্রেম](https://en.wikipedia.org/wiki/Frame_(video))। প্রতি সেকেন্ডে কতগুলো ফ্রেম দেখানো হবে তাকে বলা হয় ফ্রেম রেট যা প্রকাশ করা হয় [Frames Per Second or FPS](https://en.wikipedia.org/wiki/Frame_rate) দিয়ে।

#### **কিছু লিংক**
---
 - [Computer Architecture](http://www.labri.fr/perso/strandh/Teaching/AMP/Common/Strandh-Tutorial/Dir.html)
 - [how transistor works, an alternate viewpoint](http://amasci.com/amateur/transis.html)
 - [Zoom into a computer chip: Watch this video to fully appreciate just how magical modern microchips are](https://www.extremetech.com/extreme/191996-zoom-into-a-computer-chip-watch-this-video-to-fully-appreciate-just-how-magical-modern-microchips-are)
 - [This is What's Inside a CPU](https://www.youtube.com/watch?v=NKYgZH7SBjk)

#### **শেষের আগে**
---
যদিও 'আদ্যোপান্ত' শব্দটির অর্থ প্রথম হতে শেষ, এই লেখাটিতে মুলত আধুনিক (ইলেকট্রনিক) কম্পিউটার নিয়ে লেখা হয়েছে। আবার অনেক কিছুই এড়িয়ে যেয়ে সংক্ষেপে লিখতে হয়েছে সহজে অল্প কথায় বোঝানোর জন্য। এর মাঝে কম্পিউটার এর অনেক ইতিহাসও বাদ পরেছে। কতশত গনিতবিদ, বিজ্ঞানী, ইঞ্জিনিয়ার দের মেধা, পরিশ্রম আর প্রচেষ্টায় আজকের এই বিস্ময়কর যন্ত্র টি আমাদের হাতের মুঠোয়। কিন্তু কি নিদারুণ নির্বুদ্ধিতায় আমরা এই আশ্চর্য আবিষ্কারটি প্রতিনিয়ত অপব্যবহার করে যাচ্ছি!!

<script>
hljs.initHighlightingOnLoad();
</script>
