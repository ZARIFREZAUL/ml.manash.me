> “Give me six hours to chop down a tree and I will spend the first four sharpening the axe.” 
― Abraham Lincoln

***

# ডেটা প্রস্তুত করা (ডেটা কালেকশন ও প্রিপ্রসেসিং) - ১

আমরা আগের পর্বে দেখেছি সঠিক প্রশ্নের মাধ্যমে আমাদের টার্গেট স্টেটমেন্ট তৈরি করে কীভাবে।

আমরা আজকে মেশিন লার্নিংয়ের দ্বিতীয় ধাপ দেখব। দ্বিতীয় ধাপে ছিল,

![prepare_data_workflow](http://i.imgur.com/qTjV2Wi.jpg)


মেশিন লার্নিং মানেই ডেটা নিয়ে কাজ কারবার, তাই আমি যদি বলি, ডেটা সংগ্রহ, প্রসেস করতেই মডেল বিল্ডিংয়ের সবচেয়ে বেশি সময় ব্যয় হয় সেটা আশ্চর্যের কিছু নয়।

মডেল বিল্ড হবে সংগ্রহ করা ডেটার উপর, আপনার অ্যালগরিদম যতই ভাল হোক, ডেটা যদি কার্যকর না হয় তবে আপনার প্রেডিক্টিভ মডেলও ভাল হবে না। এটা সর্বসম্মতিক্রমে স্বীকৃত। তাই মেশিন লার্নিংয়ের এই ধাপ এ আপনাকে বেশি বেশি যত্নবান হতে হবে।

আবার ডেটা প্রস্তুতকরণ যদি ভাল হয় তবে মডেল তৈরি করা অনেকটা সহজ হবে, বারবার টিউনিংয়ের দরকার হবে না এবং ডেটা ক্লিনিংয়েরও প্রয়োজন হবে না। যদি ডেটা ভালভাবে প্রস্তুত না করতে পারেন, তাহলে আপনার মডেল তো ভাল হবেই না, বার বার ডেটায় হাত দিতে হবে মডেল বিল্ডিংয়ের জন্য।

তাই আগে ডেটা ক্লিন করে ম্যানেজেবল পর্যায়ে নিয়ে মডেল বিল্ডিংয়ে হাত দেওয়া ভাল।

দেখা যাক এই পর্বে আমরা কী করব।

## ওভারভিউ

* ডেটা খোঁজা
* ডেটা পর্যবেক্ষণ (Inspection) ও অপ্রয়োজনীয় অংশ বাদ দেওয়া (Data Cleaning)
* ডেটা এক্সপ্লোর করা (Data Exploration)
* ডেটা মোল্ডিংয়ের মাধ্যমে Tidy Data তে কনভার্ট করা
* সবকাজগুলো Jupyter Notebook এ করা

আগে দেখা যাক, Tidy Data কী?

### Tidy Data

 যে ডেটাসেট দিয়ে সহজে মডেল তৈরি করা যায়, সহজে ভিজুয়ালাইজ করা যায় এবং যাদের একটা নির্দিষ্ট স্ট্রাকচার বা গঠন আছে সেগুলোই হচ্ছে Tidy Data.

### Tidy Data এর বৈশিষ্ট্য
* প্রত্যেকটা variable হবে একেকটা column
* প্রত্যেকটা observation হবে একেকটা row
* প্রত্যেকটা observational unit হবে একেকটা table

সংগ্রহকৃত ডেটাসেট কে Tidy ফর্মে নেয়া কিছুটা সময়সাপেক্ষ।

মেশিন লার্নিং বেজড প্রজেক্টগুলোতে ৫০-৮০% সময় ব্যয় হয় ডেটা সংগ্রহ, ক্লিনিং আর অর্গ্যানাইজ করতে।

***

## ডেটা সংগ্রহ

### ডেটা সংগ্রহের ভাল উৎস কোনগুলো?
  * **Google**

    * গুগলে সার্চ দিলে অবশ্যই পাবেন, তবে একটু সাবধান, হাবিজাবি, ফেক আর বাতিল ডেটাও সেখানে থাকতে পারে, টেস্টিংয়ের জন্য সেগুলো ব্যবহার করা যেতেই পারে। কিন্তু কোন সিরিয়াস প্রজেক্ট করলে অবশ্যই ভেরিফাইড ডেটা সংগ্রহ করার চেষ্টা করবেন।


  * **সরকারি ডেটাবেজ**

    * ডেটা কালকেশনের জন্য সরকারি ডেটাবেজগুলো আসলেই ভাল উৎস। কারণ এখানে আপনি মোটামুটি ভেরিফাইড ডেটাই পাবেন বলে ধরা যায়। কিছু কিছু সরকারি ডেটাবেজের সাথে ভাল ডকুমেন্টেশনও থাকে ডেটা চিনিয়ে দেওয়ার জন্য।


  * **প্রফেশনাল বা কোম্পানির ডেটা সোর্স**

    * খুবই ভাল একটা সোর্স। বেশ কিছু প্রোফেশনাল সোসাইটি তাদের ডেটাবেজ শেয়ার করে। টুইটার তাদের টুইট এর কালেকশন ও সেসব টুইটের নিজস্ব অ্যানালাইসিস রিপোর্ট ও শেয়ার করে থাকে। ফাইন্যান্সিয়াল ডেটা পাওয়া যায় কোম্পানির ফ্রি API থেকে, যেমন Yahoo! এই ধরণের ডেটাসেট শেয়ার করে।


  * **আপনি যে কোম্পানিতে কাজ করেন**

      * আপনি যে কোম্পানিতে আছেন সেটাও ডেটার একটা ভাল উৎস হতে পারে।


  * **ইউনিভার্সিটির ডেটা রিপোজিটরি**

    * বেশ কিছু ইউনিভার্সিটি ফ্রি তে ডেটাসেট দিয়ে থাকে, যেমন University of California Irvine। এদের নিজস্ব ডেটা রিপোজিটরি আছে যেখান থেকে আপনি ডেটা কালেক্ট করতে পারবেন।


  * **[Kaggle](http://www.kaggle.com)**

    * মেশিন লার্নিং নিয়ে কাজ করবেন অথচ Kaggle এর নাম জানবেন না তা হয় না। একে ডেটা সাইন্টিস্টদের codeforce বলতে পারেন। ডেটা অ্যানালাইসিস নিয়ে নিয়মিত কন্টেস্ট হয় ওখানে। হাই গ্রেড ডেটাসেট এর জন্য অতুলনীয়।


  * **[GitHub](http://www.github.com)**

    * জ্বি হ্যাঁ, গিটহাবেও প্রচুর পরিমানে ডেটা পাওয়া যায়। [এই Awesome Dataset Collection চেক করতে পারেন](https://github.com/caesar0301/awesome-public-datasets)


  * **উপরে যেগুলো আলোচনা করা হয়েছে সবগুলাই**

    * কখনো কখনো একটা সোর্সের ডেটা দিয়ে কাজ হয় না, তখন সবগুলা সোর্স ই ট্রাই করবেন আরকি। তারপর সব ডেটা ইন্টিগ্রেট করে Tidy ডেটা বানিয়ে কাজ করতে হবে।


***

## আমাদের নির্বাচিত সমস্যার ডেটাসেট কোথা থেকে সংগ্রহ করব?

## [Pima Indian Diabetes Data](https://archive.ics.uci.edu/ml/machine-learning-databases/pima-indians-diabetes/)

* #### [ডেটা ফাইল](https://archive.ics.uci.edu/ml/machine-learning-databases/pima-indians-diabetes/pima-indians-diabetes.data)
* #### [ডেটাসেট বিবরণ](https://archive.ics.uci.edu/ml/machine-learning-databases/pima-indians-diabetes/pima-indians-diabetes.names)

আগেই বলা হয়েছে ডায়বেটিস এর ডেটাবেজ আমরা সংগ্রহ করব UCI Machine Learning রিপোজিটরি থেকে।

এই ডেটাসেট এর কিছু বৈশিষ্ট্য:
  * কমপক্ষে ২১ বছর বয়সের Female Patient
  * ৭৬৮ টা অবজারভেশন (৭৬৮ টা Row)
    *   প্রতি Row এর বিপরীতে আছে ১০ টি করে column
      * ১০ টি কলামের ৯ টি হল Feature, মানে : Number of pregnencies, blood pressure, glucose, insuline level ... ইত্যাদি
      * আর বাকি ১টা কলাম হল: ডায়বেটিস আছে কি নাই (True / False)


এই ডেটাসেট ব্যবহার করে আমরা প্রবলেম এর সল্যুশন বের করব।

তার আগে কিছু ডেটা রুল দেখে নেয়া যাক।

### Data Rule #1

> আপনি যা প্রেডিক্ট করতে চাইছেন, ডেটাসেট এ সেটা যতটা স্পষ্ট থাকবে ততটাই ভাল

রুল টা পড়তে বা শুনতে মনে হতে পারে এই রুল আর এমনকি, সাধারণ জ্ঞান দিয়েই তো বোঝা যায়।

আসলে ব্যাপারটা তা না, আমরা যেহেতু বের করতে চাচ্ছি একজন লোকের ডায়বেটিসে আক্রান্ত হওয়ার সম্ভাবনা কত সেহেতু এই ডেটাসেট আমাদের কাজের জন্য পার্ফেক্ট, কেননা একটি কলামে ডিরেক্টলি দেওয়াই আছে, যে ব্যক্তিকে পরীক্ষা করা হয়েছে তিনি ডায়বেটিসে আক্রান্ত কিনা?

অনেক সমস্যার সমাধান করতে গেলে আপনি ঠিক যে জিনিস টা প্রেডিক্ট করতে চাচ্ছেন সেটা ডেটাসেট এ আলাদা করে নাও পেতে পারেন। তখন আপনাকে ডেটাসেট নতুন করে সাজাতে হবে এবং এমনভাবে সাজাতে হবে যেটা আপনার টার্গেট ভ্যারিয়েবল (যে অ্যাট্রিবিউট প্রেডিক্ট করবেন, যেমন এখানে ডায়বেটিস আছে কি নাই) এর সাথে মিলে যায় বা কাছাকাছি আসে।

### Data Rule #2

> ডেটাসেট দেখতে যতটাই সুশ্রী মনে হোক না কেন, আপনি যেভাবে সেটা দিয়ে কাজ করতে চান সেটা কখনোই ওই ফরম্যাটে থাকবে না।

তাই ডেটা সংগ্রহের পরবর্তী কাজ হল ডেটা প্রিপ্রসেসিং। যেটা নিয়ে আমরা আজকে আলোচনা করব।


***

## CSV (Comma Separated Value) ডেটা ফাইল ডাউনলোড ও নির্দেশনা

যদি আপনি UCI এর লিঙ্কে গিয়ে ভিসিট করে থাকেন তাহলে দেখবেন সেখানে `.data` ও `.name` নামের দুইটা ফাইলের লিঙ্ক দেওয়া আছে।

`.data` ফাইলে ভ্যালুগুলো কমা সেপারেটেড আছে কিন্তু ফাইল ফরম্যাট `.csv` নয়, আরেকটি ব্যাপার হল সেখানে ভ্যালু কোনটার মানে কী সেটাও বলা নেই (বলা আছে তবে আলাদা ফাইলে - `.name`)।

তাই আপনাদের কাজের সুবিধার জন্য আমি `.csv` ফাইলটি আপলোড করে দিয়েছি। যেখানে ভ্যালুর পাশাপাশি কোন কলাম আসলে কোন প্রোপার্টি নির্দেশ করে সেটাও বলা আছে।

দুইটা ফাইল-ই ডাউনলোড করে আপনার পিসিতে রাখুন।

* [csv pima dataset ডাউনলোড (original)](https://raw.githubusercontent.com/howtocode-com-bd/ml.howtocode.com.bd/master/datasets/pima%20diabetes%20data/pima-data-orig.csv)

* [csv pima dataset ডাউনলোড (modified)](https://raw.githubusercontent.com/howtocode-com-bd/ml.howtocode.com.bd/master/datasets/pima%20diabetes%20data/pima-data.csv)


##### নোট
* *original :* এখানে ডায়বেটিস আছে কি নাই সেটা বলা হয়েছে `1/0` দিয়ে
* *modified :* সকল `1/0` কে `TRUE/FALSE` দিয়ে রিপ্লেস করা হয়েছে

***

## Pandas লাইব্রেরি দিয়ে ডেটা এক্সপ্লোরেশন


ipython notebook সম্পর্কে কিছুটা জেনেছেন তো? না জেনে থাকলে [এখান থেকে](http://ml.howtocode.com.bd/module_intro/ipython_notebook.html) একবার দেখে নিন।

* উইন্ডোজে থাকলে `cmd` ওপেন করুন ও নিচের কমান্ড দিয়ে নোটবুক ওপেন করুন
   * `ipython notebook`
   * যদি ওই কমান্ড না কাজ করে তাহলে এটা ট্রাই করুন `jupyter notebook`

![ipython](http://i.imgur.com/RfREmVD.gif)




* আপনার ব্রাউজার ওপেন হলে `New > Python 2` একটি পাইথন ফাইল ওপেন করুন আর এখানে দেখানো কাজগুলো করে ফেলুন।

![ipython2](http://i.imgur.com/u70wHTS.gif)


### প্রয়োজনীয় লাইব্রেরি ইম্পোর্ট

কাজ শুরু করার আগে নিচের কোড দিয়ে আমরা প্রয়োজনীয় লাইব্রেরি গুলো অ্যাড করে নিলাম

```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

#ইনলাইন প্লটিংয়ের জন্য জুপিটার নোটবুকের ম্যাজিক ফাংশন (আলাদা উইন্ডোতে প্লট শো করতে চাচ্ছি না আমরা)
%matplotlib inline
```

### ডেটা লোড ও রিভিউ

![import](http://i.imgur.com/egqIvbd.gif)

#### `pd.read_csv('file_path')`

আমরা এখানে `pandas` লাইব্রেরি কে `pd` হিসেবে (`as`) ইম্পোর্ট করেছি, তারমানে `pandas` এর কোন ফাংশন কল করার জন্য আমার `pandas` কথাটা পুরা লেখার দরকার নাই, `pd` লিখলেই হবে।

আমি যদি এটা করতাম,

```python
import pandas as PANDA
```

তাহলে ফাংশন কল করার জন্য `PANDA.read_csv('file_path')` এভাবে লিখতাম।

এবার আসি `read_csv` ফাংশনে, ফাংশন থেকে বোঝা যায় এর কাজ হচ্ছে `csv` ফাইল রিড করা।

এই ফাংশন `csv` ফাইলকে কনভার্ট করে `Pandas` ডেটাফ্রেম ফরম্যাটে পরিণত করে। যেটার বিভিন্ন ধরণের পরিবর্তন আমরা `Pandas` লাইব্রেরি দিয়েই করতে পারব।

`read_csv('filePath')` এখানে আমি আর্গুমেন্টে আমার পিসির যেখানে `csv` ফাইল ছিল সেই ডিরেক্টরি দিয়েছি। আপনার ক্ষেত্রে অবশ্যই আপনার পিসির যেখানে ফাইলটা আছে সেই ডিরেক্টরি দিতে হবে।

#### ‍‍`data_frame.shape`

ডেটাফ্রেমের ডেটা যেহেতু একটি ম্যাট্রিক্স (বা 2D Array) তাই আমরা এর Row আর Column সংখ্যা দেখার জন্য `shape` ভ্যারিয়েবলটি কল করেছি।

আউটপুট Row - 768 (লেবেল ছাড়া) আর Column - 10 টা

#### `data_frame.head(number)`

`data_frame.head(3)` ফাংশনটি কল করার মাধ্যমে আমরা ডেটাফ্রেমের প্রথম ৩ টি রো প্রিন্ট করলাম।

#### `data_frame.tail(number)`

`data_frame.tail(4)` ফাংশনটি কল করার মাধ্যমে আমরা ডেটাফ্রেমের শেষের ৪টি Row প্রিন্ট করলাম।

***

আজকের চ্যাপ্টার এখানেই শেষ, তবে এটা ডেটা প্রিপ্রসেসিংয়ের প্রথম অংশ ছিল। পরবর্তী পর্বে আমরা ডেটা প্রিপ্রসেসিংয়ের ফান্ডামেন্টাল বিষয় গুলো নিয়ে আলোচনা করব।
