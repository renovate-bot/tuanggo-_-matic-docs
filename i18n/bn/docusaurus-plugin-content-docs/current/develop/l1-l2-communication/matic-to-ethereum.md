---
id: matic-to-ethereum
title: Polygon থেকে Ethereum-এ ডেটা ট্রান্সফার
description: চুক্তির মাধ্যমে Polygon থেকে Ethereum-এ স্টেট বা ডেটা ট্রান্সফার
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Polygon থেকে Ethereum-এ ডেটা ট্রান্সফার করার প্রক্রিয়াটি Ethereum থেকে Polygon-এ ট্রান্সফার করার প্রক্রিয়াটি থেকে কিছুটা ভিন্ন। Ethereum চেইনে যাচাইকারী দ্বারা তৈরি **চেকপয়েন্ট** লেনদেনগুলো এটি অর্জন করতে ব্যবহৃত হয়। মূলত Polygon-এ প্রথমে লেনদেন তৈরি করা হয়। এই লেনদেনটি তৈরি করার সময়, এটি নিশ্চিত করতে হবে যে একটি **ইভেন্ট প্রেরিত হয়েছে** এবং **ইভেন্টের লগ-এ Polygon থেকে Ethereum-এ ট্রান্সফার করতে ইচ্ছুক এমন ডেটা অন্তর্ভুক্ত রয়েছে।**

একটি সময়ে ( প্রায় 10-30 মিনিট ), যাচাইকারী কর্তৃক Ethereum চেইনে এই লেনদেনটি চেক-পয়েন্ট করা হয়। চেকপয়েন্টের কাজ শেষ হওয়ার পর, Polygon চেইনে তৈরি হওয়া লেনদেনের হ্যাশটি Ethereum চেইনে  **RootChainManager** চুক্তিতে একটি প্রমাণ হিসেবে জমা দেওয়া যাবে। এই চুক্তিটি লেনদেনটি যাচাই করে, এই লেনদেনটি চেকপয়েন্টে অন্তর্ভুক্ত রয়েছে কি না তা যাচাই করে এবং পরিশেষে এই লেনদেনটি থেকে ইভেন্টের লগগুলো ডিকোড করে।

এই পর্যায়টি শেষ হওয়ার পরে, Ethereum চেইনে ডিপ্লয় করা রুট চুক্তিতে **কোনো পরিবর্তন করতে আমরা ডিকোড করা ইভেন্টের লগের ডেটা** ব্যবহার করতে পারি। এর জন্য আমাদেরকে আরো নিশ্চিত করতে হবে যে, Ethereum-এ স্টেটের পরিবর্তন কেবল একটি নিরাপদ পদ্ধতিতে সম্পন্ন হয়েছে। সুতরাং, আমরা একটি **নিশ্চিত** চুক্তি ব্যবহার করি, যা একটি বিশেষ ধরনের চুক্তি যা শুধুমাত্র **RootChainManager** চুক্তি দ্বারা ট্রিগার করা যেতে পারে। এই আর্কিটেকচারটি নিশ্চিত করে যে Ethereum-এ স্টেটের পরিবর্তন শুধুমাত্র তখনই ঘটে যখন Polygon-এ লেনদেনটি চেক পয়েন্ট করা হয় এবং **RootChainManager** চুক্তি দ্বারা Ethereum চেইনে যাচাই করা হয়।

# সংক্ষিপ্ত বিবরণ {#overview}

- Polygon চেইনে ডিপ্লয় করা চাইল্ড চুক্তিতে একটি লেনদেন সম্পন্ন করা হয়।
- এই লেনদেনে একটি ইভেন্টও প্রেরিত হয়। এই ইভেন্টের প্যারামিটারে সেসকল **ডেটা অন্তর্ভুক্ত থাকে যা Polygon থেকে Ethereum-এ ট্রান্সফার করতে হবে**।
- Polygon নেটওয়ার্কে যাচাইকারী এই লেনদেনটি নির্দিষ্ট সময়ের ব্যবধানে ( সম্ভবত 10-30 মিনিট) সংগ্রহ করে এবং Ethereum-এ **সেগুলোকে চেকপয়েন্টে যোগ করে।**
- **RootChain** চুক্তিতে একটি চেকপয়েন্ট লেনদেন তৈরি হয় এবং এই [স্ক্রিপ্ট](https://github.com/rahuldamodar94/matic-learn-pos/blob/transfer-matic-ethereum/script/check-checkpoint.js) ব্যবহার করে চেকপয়েন্টের অন্তর্ভুক্তি চেক করা যেতে পারে
- চেকপয়েন্টের যোগ সম্পন্ন হওয়ার পরে, **matic.js** লাইব্রেরিটি **RootChainManager** চুক্তির **বের হওয়ার** ফাংশনটিকে কল করতে ব্যবহার করা যেতে পারে। **বের হওয়ার** ফাংশনটি matic.js লাইব্রেরি ব্যবহার করে কল করা যেতে পারে যেমনটি এই [উদাহরণে](https://github.com/rahuldamodar94/matic-learn-pos/blob/transfer-matic-ethereum/script/exit.js) দেখানো হয়েছে।

- স্ক্রিপ্টটি চালালে, Ethereum চেইনে Polygon লেনদেনের হ্যাশ অন্তর্ভুক্ত করার বিষয়টি যাচাই করা যায় এবং তারপর পর্যায়ক্রমে [নিশ্চিত](https://github.com/rahuldamodar94/matic-learn-pos/blob/transfer-matic-ethereum/contracts/CustomPredicate.sol) চুক্তির **exitToken** ফাংশনকে কল করে।
- এটি নিশ্চিত করে যে **রুট চেইন চুক্তিতে স্টেটের পরিবর্তন** সবসময় **নিরাপদ** উপায়ে এবং **শুধুমাত্র নিশ্চিত চুক্তির মাধ্যমে** সম্পন্ন হয়।
- যে বিষয়টি উল্লেখ করা গুরুত্বপূর্ণ তা হলো Polygon থেকে **হ্যাশ করা লেনদেন যাচাইকরণ** এবং **নিশ্চিত করা চুক্তিটি ট্রিগার করা** একটি **একক লেনদেনে** ঘটে থাকে এবং এইভাবে রুট চুক্তিতে কোনো স্টেটের পরিবর্তনের নিরাপত্তা নিশ্চিত করে।

# বাস্তবায়ন {#implementation}

Polygon থেকে Ethereum-এ ডেটা কীভাবে ট্রান্সফার করা যেতে পারে এটি তার একটি সাধারণ উদাহরণ। এই টিউটোরিয়ালে পুরো চেইনে একটি uint256 মান ট্রান্সফার করার একটি উদাহরণ রয়েছে। ডেটার ধরন ট্রান্সফার করতে পারেন, তবে ডেটা বাইটে এনকোড করার পর এটি চাইল্ড চুক্তি থেকে প্রেরণ করা জরুরি। পরিশেষে এটি রুট চুক্তিতে ডিকোড করা যেতে পারে।

1. প্রথমে রুট চেইন এবং চাইল্ড চেইনের চুক্তি তৈরি করুন। যে ফাংশনটি স্টেটের পরিবর্তন করে তাও একটি ইভেন্ট থেকে প্রেরণ করার বিষয়টি নিশ্চিত করুন। এই ইভেন্টে অবশ্যই সেসকল ডেটা অন্তর্ভুক্ত থাকবে যা এর একটি প্যারামিটারে ট্রান্সফার করা হবে। চাইল্ড এবং রুট চুক্তি দেখতে অবশ্যই কেমন হতে হবে তার একটি নমুনা ফরম্যাট নিচে দেওয়া হলো। এটি একটি খুব সাধারণ চুক্তি যার ডেটার মান রয়েছে এবং যার মান একটি setData ফাংশন ব্যবহার করে নির্ধারণ করা হয়। setData ফাংশনটি কল করা হলে ডেটা ইভেন্ট প্রেরণ করে। চুক্তিতে থাকা অবশিষ্ট বিষয়গুলো এই টিউটোরিয়ালের আসন্ন বিভাগে ব্যাখ্যা করা হবে।

A. চাইল্ড চুক্তি

```javascript
contract Child {

    event Data(address indexed from, bytes bytes_data);

    uint256 public data;

    function setData(bytes memory bytes_data) public {
     data = abi.decode(bytes_data,(uint256));
     emit Data(msg.sender,bytes_data);
    }

}
```

B. রুট চুক্তি

রুট চুক্তি কন্সট্রাক্টরে `_predicate`-এর মান হিসেবে এই `0x1470E07a6dD1D11eAE439Acaa6971C941C9EF48f` পাস করুন।

```javascript
contract Root {

    address public predicate;
    constructor(address _predicate) public{
        predicate=_predicate;
    }

   modifier onlyPredicate() {
        require(msg.sender == predicate);
        _;
    }

    uint256 public data;

    function setData(bytes memory bytes_data) public onlyPredicate{
        data = abi.decode(bytes_data,(uint256));
    }

}
```

2. চাইল্ড এবং রুট চুক্তি যথাক্রমে Polygon এবং Ethereum চেইনে ডিপ্লয় করা হলে, এই চুক্তিগুলো PoS ব্রিজ ব্যবহার করে ম্যাপ করতে হবে। পুরো চেইনে এই দুটি চুক্তির মধ্যে একটি সংযোগ বজায় রাখার বিষয়টি এই ম্যাপিং-এর মাধ্যমে নিশ্চিত করা হয়। এই ম্যাপিং করার জন্য, Polygon দলকে [discord](https://discord.com/invite/0xPolygon)-এ পাওয়া যাবে।

3. একটি গুরুত্বপূর্ণ বিষয় মনে রাখতে হবে যে, রুট চুক্তিতে একটি onlyPredicate মডিফায়ার রয়েছে। এই মডিফায়ারটি সবসময় ব্যবহার করার পরামর্শ দেওয়া হয়, কারণ এটি নিশ্চিত করে যে শুধুমাত্র নিশ্চিত করা চুক্তি রুটচুক্তিতে স্টেটের পরিবর্তন করে থাকে। নিশ্চিত করা চুক্তি হলো একটি বিশেষ চুক্তি, যা শুধুমাত্র Polygon চেইনে সম্পন্ন হওয়া লেনদেনটি Ethereum চেইনে RootChainManager দ্বারা যাচাই করার পরই রুট চুক্তি ট্রিগার করে। এটি রুট চুক্তিতে স্টেটের নিরাপদ পরিবর্তন নিশ্চিত করে।

উপরের বাস্তবায়নের বিষয়টি পরীক্ষা করার জন্য, আমরা চাইল্ড চুক্তির **setData** ফাংশনটি কল করে Polygon চেইনে একটি লেনদেন তৈরি করতে পারি। চেকপয়েন্টটি সম্পন্ন করার জন্য আমাদেরকে এই সময় অপেক্ষা করতে হবে। এই [স্ক্রিপ্টটি](https://github.com/rahuldamodar94/matic-learn-pos/blob/transfer-matic-ethereum/script/check-checkpoint.js) ব্যবহার করে চেকপয়েন্টের অন্তর্ভুক্তি চেক করা যেতে পারে। চেকপয়েন্টের সম্পন্ন হওয়ার পর, matic.js SDK ব্যবহার করে RootChainManager-এর বের হওয়ার ফাংশনটি কল করুন।

```jsx
const txHash =
  "0xc094de3b7abd29f23a23549d9484e9c6bddb2542e2cc0aa605221cb55548951c";

const logEventSignature =
  "0x93f3e547dcb3ce9c356bb293f12e44f70fc24105d675b782bd639333aab70df7";

const execute = async () => {
  try {
    const tx = await maticPOSClient.posRootChainManager.exit(
      txHash,
      logEventSignature
    );
    console.log(tx.transactionHash); // eslint-disable-line
  } catch (e) {
    console.error(e); // eslint-disable-line
  }
};
```

উপরের স্ক্রিনশটে যেভাবে দেখানো হয়েছে, **txHash** হলো Polygon চেইনে ডিপ্লয় করা চাইল্ড চুক্তিতে ঘটা লেনদেনের একটি লেনদেন হ্যাশ।

**logEventSignature** হলো ডেটা ইভেন্টের keccack-256 হ্যাশ। নিশ্চিত চুক্তিতে আমরা যে হ্যাশটি অন্তর্ভুক্ত করেছি এই হ্যাশটি ঠিক সেরকমই। এই টিউটোরিয়ালের জন্য ব্যবহৃত সকল চুক্তির কোড এবং বের হওয়ার স্ক্রিপ্ট [এখানে](https://github.com/rahuldamodar94/matic-learn-pos/tree/transfer-matic-ethereum) পাওয়া যাবে

বের হওয়ার স্ক্রিপ্টটি সম্পন্ন হওয়ার পরে, চাইল্ড চুক্তিতে নির্ধারিত ভ্যারিয়েবল **ডেটার** মান রুট চুক্তির **ডেটার** ভ্যারিয়েবলেও প্রতিফলিত হয়েছে কি না তা যাচাই করতে Ethereum চেইনের রুট চুক্তিটি কুয়েরি করা যাবে।
