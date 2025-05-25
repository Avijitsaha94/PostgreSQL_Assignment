1.What is PostgreSQL?
Answer: PostgreSQL হলো একটা ডাটাবেস ম্যানেজমেন্ট সিস্টেম। সহজ কথায় এটা এমন একটা সফটওয়্যার যেটা ডাটা সংরক্ষণ করে, ডাটা খুঁজে আনে এবং ডাটার উপর বিভিন্ন কাজ করতে সাহায্য করে। এটা ওপেন সোর্স অর্থাৎ বিনামূল্যে এবং অনেক শক্তিশালী। ওয়েবসাইট, অ্যাপ বা বড় বড় সফটওয়্যারে PostgreSQL ব্যবহার করা হয় ডাটা ঠিকঠাক রাখার জন্য।


2. Explain the Primary Key and Foreign Key concepts in PostgreSQL.
Answer: Primary key-প্রাইমারি কী হলো টেবিলের সেই কলাম বা কলামের সেট যেটা প্রতিটা রেকর্ডকে আলাদা করে চিহ্নিত করে। এতে কোনো ডুপ্লিকেট বা ফাঁকা (NULL) মান থাকে না।
উদাহরণ:
ধরো তোমার একটা students টেবিল আছে, সেখানে student_id হলো প্রাইমারি কী।

CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,
    name VARCHAR(50)
);
এখানে student_id হবে ইউনিক আইডি, যার মান কোনো দুইজন ছাত্রের জন্য একই হতে পারে না।

 Foreign Key-ফরেন কী হলো এমন একটা কলাম যেটা অন্য টেবিলের প্রাইমারি কী এর সাথে সম্পর্ক রাখে। এটা দুইটা টেবিলকে যুক্ত করে। অর্থাৎ, একটা টেবিলের ডাটা অন্য টেবিলের ডাটার ওপর ভিত্তি করে থাকে।
উদাহরণ:
enrollments টেবিলে student_id হলো ফরেন কী, যা students টেবিলের student_id এর সাথে যুক্ত।

CREATE TABLE enrollments (
    enrollment_id SERIAL PRIMARY KEY,
    student_id INT REFERENCES students(student_id),
    course_name VARCHAR(100)
);

3.Explain the purpose of the WHERE clause in a SELECT statement?
Answer:WHERE ক্লজ ব্যবহার করা হয় যখন আমরা ডাটাবেজ থেকে নির্দিষ্ট কিছু শর্ত অনুযায়ী ডাটা বের করতে চাই। সব ডাটা একসাথে দেখানো সব সময় দরকার হয় না। অনেক সময় দরকার হয় –

কোন নির্দিষ্ট নামের মানুষকে খুঁজে বের করা,
নির্দিষ্ট বয়সের উপরে যাদের বয়স,
কোন নির্দিষ্ট জায়গা বা সময়ের ভেতরের তথ্য ইত্যাদি।
WHERE ক্লজ মূলত ফিল্টার করার কাজ করে। সেটা SELECT, UPDATE, বা DELETE স্টেটমেন্টের সাথে ব্যবহার করা হয়।

উদাহরণ:

SELECT * FROM students WHERE name = 'Rahim';
এখানে শুধুমাত্র সেইসব ছাত্রদের তথ্য আসবে যাদের নাম 'Rahim'।

4.How can you modify data using UPDATE statements?
UPDATE কমান্ড দিয়ে টেবিলের ডাটা পরিবর্তন করা হয়। সাধারণত WHERE ক্লজ দিয়ে কোন রেকর্ড পরিবর্তন করতে হবে সেটা নির্দিষ্ট করা হয়।

উদাহরণ:

UPDATE students
SET name = 'Rahim Uddin'
WHERE student_id = 1;
এখানে যেই ছাত্রের আইডি ১, তার নাম ‘Rahim Uddin’ এ পরিবর্তিত হবে।

5.How can you calculate aggregate functions like COUNT(), SUM(), and AVG() in PostgreSQL?
Answer:Aggregate Functions ডাটার উপর গণনা করে একটা সারসংক্ষেপ মান দেয়।

COUNT() = কয়টা রেকর্ড আছে সেটা গননা করে

SUM() = কোনো সংখ্যার যোগফল বের করে

AVG() = সংখ্যাগুলোর গড় মান দেয়

উদাহরণ:
ধরা যাক তোমার একটা orders টেবিল আছে যেখানে amount নামের কলামে বিক্রির টাকা আছে।

SELECT COUNT(*) FROM orders;          
SELECT SUM(amount) FROM orders;       
SELECT AVG(amount) FROM orders;  


