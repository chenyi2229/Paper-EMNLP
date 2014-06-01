- PATTERN

	我們要解決的問題是「判斷部落格文章的情緒」
	
	前人的研究顯示：這仍然是一個很俱有挑戰性的任務 `citation?`
	
	他們用了許多 shallow features 像是 n-gram, pos tag, word frequency 來判斷文章情緒
		
	但因為部落格的文章十分接近生活口語：人們通常不會直接寫出情緒相關的字眼，反而是透過描述一個事件來表達此刻的心境
	
	例如: ....
	
	所以，我們要利用更深入的 semantic 資訊來解決問題。

	- Pattern extraction
	
		因為句子中不一定有情緒關鍵字，所以前人的研究會利用部份字組(a fragment of sentence) 試圖包圍更多的字來捕捉特定事件跟判斷情緒 `citation` 
		
		最常見的作法是用 word sequency, i.e., n-gram
		
		n-gram 的好處是 `優點1`
		
		//On one hand high-order n-grams, such as trigrams, should better capture patterns of sentiments expressions. 
		//On the other hand, unigrams should provide a good coverage of the data.		
		然而，用 n-gram 會搜集到許多不重要的資訊 
		
		造成 `缺點1` , `缺點2`, 跟 `缺點3`  
		// 缺點 1.人類無法理解的組合 
		// 缺點 2.redundance/資料龐大，
		// 缺點 3.為了計算的有效性，必須限制長度
		
		因此，根據「取部分字組來表達特定事件」這個想法
		
		我們想要找出「informative 的 multiword expression or pattern 」而不是 n-gram
		
		(開始講如何找出 informative 的 pattern?)
		
		從語言學的角度來看，通常一個句子當中，動詞跟其 argument 扮演著十分重要的角色。 `放 verb frame 相關 citation`
		
		例如
		
		I have a pretty good chance of getting accepted!  (excited)
		
		According to this results, we extract verbs and corresponding arguments by grammatical relations and semantic roles to construct verb frames, i.e., patterns. Consider this sentence, "I have a pretty good chance of getting accepted!", which is a post in Livejournal and labeled as the "excited" mood tag.
		
		// 之中，動詞 have，跟主詞 I 還有受詞 chance，可以形成一組 verb frame："I have chance"
		We identify the verb "have" along with its nominal subject "I" and direct object "chance" to form a verb-argument frame: "I, have, chance". (這句話分三部分來講？)
		
		// 別于傳統像是 "I have a", "have a pretty" 等 n-gram，
		// 對人類而言，I have chance 是可以理解，而且較貼近原本句子中想傳達思想的 multiword expression `打 n-gram 無意義`
		Different from previous approaches using n-grams, e.g., "I have a", "have a pretty" such trigrams, the verb-argument frame "I, have , chance" is more comprehenssive by human, and the meaning carried is closer to the origin sentence.
		
		In addition, it tends to use large window size when the distance between the verb and its argument increased, in this case, window size is 6 to cover the verb frame "I, have, chance"
		
		而且，如果用傳統 n-gram 的方法，當主詞或受詞距離動詞距離很長的時候，便要使用較大的 window size 才能同時 cover I ... have ... chance 這個 verb frame。In this case，必須用 6-gram   `(打 n-gram 長度問題)`
		
		因此，我們根據 verb frame 的想法，想透過  跟 semantic role 來選出跟動詞相關的 arguments		
		For this, 我們 parse sentences，用 pos tag 定位動詞，再用 semantic role label 與 grammatical relation 找出跟動詞相關的主詞、受詞、介系詞片語跟 negation 等 argument 來組成 pattern.
		
		
	- Pattern scoring

		//Formulate the emotion tendency of a pattern
		我們想要 enrich pattern 所 carry 的 emotion 資訊：e.g., 一個 pattern 在 corpus 中傾向哪個情緒 (emotion tendency)
		
		extract 出的 pattern 只帶有 surface information(feature)：POS tag, pattern count
		
		For this, we formulate the emotion tendency using a `帥氣的pattern scoring function名稱`
		
		定義問題
		
		舉例
		
		
		
		
		
===
- examples
		
		// be + adj: 形容詞會直接描述一種 mental state
		I am so happy ...
		
		// negation
		I am NOT so happy ...
		
		I did it for me. ; I did it for you. // 前者可能是自私，後面相反
		
		// 保留時態的例子
		I loved you so much ; I love you so much.


- 用 n-gram 跟 verb argument 的區別

	I think I have a pretty good chance of getting accepted (from excited/16)

	如果用 n-gram

		2-gram: good chance, chance of

		3-gram: pretty good chance, good chance of

	用 verb argument

		i have chance

		lexicon: { "hopeful" : 4, "excited" : 4, ... }

===

they __like me


I am sad
http://doraemon.iis.sinica.edu.tw/feelit/browse/pissed%20off/148/

I am ready
第一名是 hopeful (正面的情緒)


Verb frames are very important for language learners, since they capture the semantics and word usages associated with verbs

(放 introduction)
extracting verb argument tuples based on grammatical relations acquired from a parsed corpus

we generate semantic verb frames by using a parser (e.g., Stanford Parser) to obtain verbal argument tuples composed of semantic roles, such as subjects, objects, and prepositional phrases


pattern (multiword expression) 的 feature，試著在沒有情緒關鍵字的句子當中抓住作者想要表達的心境（研究的重點）

A multiword expression can be a compound, a fragment of a sentence, or a sentence


DATA SETS