<div align='center'>

# SQL কুয়েরি এক্সিকিউশন এর ধাপ সমূহ :
</div>

## Option-1 


### Sequence 

`FROM` > `JOIN` > `WHERE`> `GROUP BY` > `HAVING` > `SELECT` > `DISTINCT` > `ORDER BY` > `LIMIT`

### FROM
প্রথমে `FROM` ক্লজ কার্যকর হয়। এটি মূলত কোন টেবিল বা টেবিলগুলো থেকে ডেটা আসবে তা নির্ধারণ করে। এছাড়া টেবিল জয়েন, সাবকুয়েরি এবং অন্যান্য টেবিল অপারেশনও এই ধাপে ঘটে ।

### JOIN
`JOIN` ক্লজ `FROM` ক্লজের সাথে সম্পন্ন হয়। যদি কুয়েরিতে একাধিক টেবিল থাকে, তাহলে তাদের মধ্যে রিলেশন স্থাপন করতে JOIN কার্যকর হয়।

### WHERE
টেবিল থেকে ডেটা ফিল্টার করার জন্য `WHERE` ক্লজ কার্যকর হয়। এই ক্লজের সাহায্যে নির্দিষ্ট শর্ত অনুযায়ী ডেটা সিলেক্ট করা হয়।

### GROUP BY
`GROUP BY` ক্লজ কার্যকর হয় `WHERE` ক্লজের পর। এটি ডেটা গ্রুপ করার জন্য ব্যবহার করা হয়, যাতে একটি নির্দিষ্ট কলামের উপর ভিত্তি করে রেকর্ডগুলোকে গ্রুপ করা যায়।

`HAVING`
`GROUP BY` ব্যবহারের পর `HAVING` ক্লজ কার্যকর হয়। এটি গ্রুপ করা ডেটার উপর আরও নির্দিষ্ট শর্ত আরোপ করতে ব্যবহার করা হয়।

### SELECT
`SELECT` ক্লজ কার্যকর হয় উপরের সব ফিল্টারিং ও গ্রুপিং শেষ হওয়ার পর। এটি নির্ধারণ করে কোন কোন কলাম কুয়েরির ফলাফল হিসেবে দেখানো হবে।

### DISTINCT
`DISTINCT` ক্লজ `SELECT` এর পরে কার্যকর হয়। এটি ডুপ্লিকেট রেকর্ড সরিয়ে দেয় এবং ইউনিক রেকর্ড প্রদর্শন করে।

### ORDER BY
`ORDER BY` ক্লজ কার্যকর হয় `SELECT` ও `DISTINCT` এর পরে। এটি কুয়েরির ফলাফলকে নির্দিষ্ট ক্রমানুসারে সাজায়, যেমন ASC (Ascending) বা DESC (Descending)।

### LIMIT/OFFSET
সর্বশেষে `LIMIT` এবং `OFFSET` ক্লজ কার্যকর হয়। `LIMIT` ক্লজ দ্বারা রেকর্ডের সংখ্যা সীমাবদ্ধ করা যায় এবং `OFFSET` ব্যবহারে শুরু থেকে নির্দিষ্ট সংখ্যক রেকর্ড বাদ দিয়ে বাকি রেকর্ড দেখানো যায়।


## Courtesy By

[Shafiqul Islam Shafiq](https://www.facebook.com/shafiqpabna/)


<br>
<br>


## Option-2

![Demo Animation](/assets/sql-query-logical-order.gif)