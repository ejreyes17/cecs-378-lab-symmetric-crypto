# CECS 378 Lab: Symmetric Cryptography

## Assignment Description

This assignment is designed to allow you to get some practice with cryptanalysis of substitution ciphers. Write a program that will attempt a brute-force decryption attack on an encrypted phase that uses the simple substitution cypher. The following encrypted quotations are provided for you to test out your code (and I will attempt to run and evaluate your program using these phrases). Your program *must* make an honest attempt at cracking the phrases--any pre-programming of the resulting phrases that will "match" when the program is run will result in zero points being assigned for the lab. You may use any programming language that you like for your submission, but I recommend using something that makes text manipulation easy, like *Python*.

1. `nyyfp jxflw jfyij fqtkg wfajw dytxy fsizu yttzw jsjrn jxgzy ozxyf xrzhm ytxyf sizuy ttzwk wnjsi x`

2. `skses faexd wkzsf vtdgg vausf twayf gjwva usftw vwklj gqwvt mlsks kqetg dsksk qetgd ausft wafug jjmhl atdwa usftw wnwjd sklaf y`

3. `nfrdf rqqfl abfoj fdfsy orcsy xrcwz hrbdf qxfms qsyyk djyhy dfoof rorho cfszs qjykb oafhy sfosj rszhs jflzo qsywy kdqyd dynsj zqofr sjsrg fqxbr mfzhs jfqjr oynyw hfnbz wfsjf qkhdz qfywr hfnny dborn ydbos jrsyk dafby ufomy ldrof erufj zqbzw fsyxd ysfms rhohy kdzqj jfozo hyswf fbsjz qqrmd zwzmf rurzh ydflx scyhf rhonf nzbbh ysofa rsfjz qxdyw ykhon zqoyl rssjf qfxdy mffoz heqyw lcwdz fhozm rhyhb cqrcs jzqyw rbbsj fqykb qzjru ffhmy khsfd fozhl csdru fbqjz qnrqs jflyq sjklr h`

4. `sdfwd ridss dfwsx nsels xwkgw lsedi uxwsx wrsel idfcw reisx wveit sdlgj jwrsx wlcei plnit nrrdu ldjdg srnpw dgljd rsgiw drsds nqwnr vlnpn eilsn lwndj srdgf cwlni tfhdz zdlei pwits xwvsd tewsd lcwwz idvdr wnitf hnlcw wzsdl nhuww itsxw xwnrs nyxwn itsxw sxdgl nitin sgrnc lxdyq lsxns jcwlx elxwe rsdse lnydi lgvvn sedit wmdgs chsdf wuelx`

Additionally, you must write two smaller programs. The first will be a simple-substitution encrypter that will take in two arguments: an existing plain-text phrase and a key in the form of the modified alphabet. The second will be a decrypter for the same type of crypto and take in the encrypted phrase and the modified alphabet "key" as arguments.

Use the two smaller programs that you write to encrypt the following phrases. Make sure to provide me with the keys that you use and the resulting crypto phrase:

1. `He who fights with monsters should look to it that he himself does not become a monster. And if you gaze long into an abyss, the abyss also gazes into you.`

2. `There is a theory which states that if ever anybody discovers exactly what the Universe is for and why it is here, it will instantly disappear and be replaced by something even more bizarre and inexplicable. There is another theory which states that this has already happened.`

3. `Whenever I find myself growing grim about the mouth; whenever it is a damp, drizzly November in my soul; whenever I find myself involuntarily pausing before coffin warehouses, and bringing up the rear of every funeral I meet; and especially whenever my hypos get such an upper hand of me, that it requires a strong moral principle to prevent me from deliberately stepping into the street, and methodically knocking people's hats off - then, I account it high time to get to sea as soon as I can.`

Kudos if you can tell me who said these quotes without searching the Internet for them.

## Deliverables

Submit your source code through your git repository along with the decrypted phrases in `*.txt` format. Your submission must follow the following rules, else *I will not grade it and you will receive a zero for the submission*:

* Do not use compression on your files
* Make sure that all significant code is *commented* with your own explanations
