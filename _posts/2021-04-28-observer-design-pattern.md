---
layout: post
title: অবজার্ভার ডিজাইন প্যাটার্ন  উইথ টাইপস্ক্রিপ্ট
subtitle: Design pattern
cover-img: /assets/img/Untitled Diagram-Page-2.png
share-img: 
tags: [Design Pattern,OOP, Typescript, Observer Design Pattern]
---

অবজার্ভার ডিজাইন প্যাটার্ন কি, কিভাবে কাজ করে এবং কেন ব্যবহার করবো তা বুঝার আগে চলুন কিছু সিনারিও দেখে আসি। 
অনেক ওয়েবসাইটে নিউজলেটার নামে একটা অপশন আমরা দেখে থাকি। আমরা যদি আমাদের ইমেইল দিয়ে সেটা সাবস্ক্রাইব করি তাহলে ঐ ওয়েবসাইটে নতুন কিছু কন্টেন্ট আপডেট হলে আমাদের কাছে নোটিফিকেশন আসে। তারপর আমরা সোশ্যাল মিডিয়ায় অনেক সেলেব্রিটি বা পেজকে ফলো করি। ফলো করার জন্য আমাদের ফলো অপশনে ক্লিক করতে হয়। ফলো করার পর যদি ঐ সেলেব্রিটি বা পেজ নতুন কিছু আপলোড করে তাহলে সব ফলোয়ারের কাছে নোটিফিকেশন চলে যায়। তাছাড়া আমরা অনেকেই লিঙ্কডইনে বিভিন্ন ক্রাইটেরিয়া সেট করে জব এলার্ট অপশন অন করে রাখি।যখনই কোনো নতুন জব কেউ পোস্ট করে লিঙ্কডইন তখন নোটিফাই করে।
যদি আমরা এই সবগুলো সিনারিওর দিকে তাকাই তাহলে একটা প্যাটার্ন দেখতে পাই। সবগুলোতেই আমাদেরকে ফলো, লাইক বা সাবস্ক্রাইব করে রাখতে হয় আর যখনই নতুন কিছু আসে তখনই সেটা সবার কাছে নোটিফিকেশন আকারে পৌঁছে যায়। তো যদি এই লাইক, ফলো বা সাবস্ক্রাইব অপশন না থাকতো তাহলে কি হতো। তখন ইউজার নতুন কিছু আসছে কি না সেটা দেখার জন্য বারবার কিছুক্ষন পরপর গিয়ে দেখা লাগতো যে নতুন কোনো কিছু আসছে কি না। তাছাড়া কেউ যদি লাইভ কিছু করে সেগুলো মিস হয়ে যাওয়ার সম্ভাবনা থেকে যায়।
উপরে যে যে সিনারিওগুলো দেখলাম এই সবগুলো সমস্যার সমাধান অবজার্ভার ডিজাইন প্যাটার্ন দিয়ে করা সম্ভব। তাহলে চলুন শুরু করি

উপরের প্রত্যেকটি সিনারিওতেই যদি আমরা খেয়াল করি তাহলে দেখবো ২টি অবজেক্ট আছে। একটি হলো সাবজেক্ট অবজেক্ট যেটা উপরের প্রথম সিনারিওতে ওয়েবসাইট, দ্বিতীয় সিনারিওতে সেলিব্রেটির প্রোফাইল বা পেজ আর তৃতীয় সিনারিওতে  লিঙ্কডইন। আর আরেকটা অবজেক্ট হলো ডিপেন্ডেন্সি অবজেক্ট বা অবজার্ভার যেটা উপরের তিনটি সিনারিওতেই ইউজার যারা লাইক, ফলো বা সাবস্ক্রাইব করে রাখে। অবজার্ভার প্যাটার্ন এই দুইটি অবজেক্ট এর মধ্যে ওয়ান টু মেনি রিলেশন তৈরি করে যাতে যখনই সাবজেক্টের মধ্যে কোনো নতুন চেঞ্জ আসবে সাথে সাথে ওই সাবজেক্টের সব ডিপেন্ডেন্সি অবজেক্টকে নোটিফাই এবং আপডেট করে ফেলবে অটোম্যাটিকেলি। 


তাহলে এই সাবজেক্টের কাজ কি কি সেটা একটু চিন্তা করি। নতুন ইউজার এড করার জন্য সাবজেক্টের একটা মেথড লাগবে যেটা দিয়ে ইউজার লাইক, ফলো বা সাবস্ক্রাইব করতে পারে। একইভাবে আরেকটি অপশন লাগবে যেটা দিয়ে আনলাইক, আনফলো বা আনসাবস্ক্রাইব করতে পারবে। আরেকটি মেথড লাগবে সবাইকে নোটিফাই করার জন্য যাতে যখনই নতুন কিছু আপডেট আসবে তখনই এই মেথড কল করে সবাইকে নোটিফাই করা যায়। এই তিনটি কাজ করার জন্য আমরা তিনটি মেথড ডিফাইন করতে পারি। ক্লাস ডায়াগ্রামে আমরা সাবজেক্ট ইন্টারফেস দিয়ে এই তিনটি মেথড ডিফাইন করে দিয়েছি।
এখন আসি ডিপেন্ডেন্সি অবজেক্ট বা অবজার্ভারের কাজ কি।আমাদের অবজার্ভারকে বলে দিতে হবে সাবজেক্ট কিভাবে অবজার্ভারকে নোটিফাই করবে। এই কাজটি করার জন্য অবজার্ভারের একটি আপডেট মেথড লাগবে যেটা ব্যবহার করে সাবজেক্ট তাকে নোটিফাই করবে। ক্লাস ডায়াগ্রামে আমরা অবজার্ভার ইন্টারফেস দিয়ে এই মেথড ডিফাইন করে দিয়েছি।

আমি এই ক্লাস ডায়াগ্রামটা নিয়েছি হেড ফার্স্ট ডিজাইন প্যাটার্ন বই থেকে যেটা ডিজাইন প্যাটার্নের জন্য টপ লিস্টেড বইগুলোর মধ্যে একটি।
![alt text](/assets/img/observer1.png "Class Diagram") 