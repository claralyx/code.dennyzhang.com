# Leetcode: Short Encoding of Words     :BLOG:Medium:


---

Short Encoding of Words  

---

Similar Problems:  
-   [Review: Trie Tree Problems](https://code.dennyzhang.com/review-trie)
-   Tag: [#trie](https://code.dennyzhang.com/tag/trie)

---

Given a list of words, we may encode it by writing a reference string S and a list of indexes A.  

For example, if the list of words is ["time", "me", "bell"], we can write it as S = "time#bell#" and indexes = [0, 2, 5].  

Then for each index, we will recover the word by reading from the reference string from that index until we reach a "#" character.  

What is the length of the shortest reference string S possible that encodes the given words?  

Example:  

    Input: words = ["time", "me", "bell"]
    Output: 10
    Explanation: S = "time#bell#" and indexes = [0, 2, 5].

Note:  

-   1 <= words.length <= 2000.
-   1 <= words[i].length <= 7.
-   Each word has only lowercase letters.

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/short-encoding-of-words)  

Credits To: [leetcode.com](https://leetcode.com/problems/short-encoding-of-words/description/)  

Leave me comments, if you have better ways to solve.  

    // Blog link: https://code.dennyzhang.com/short-encoding-of-words
    // Basic Ideas: Trie (One pass, instead of two)
    //     Reverse the words, build trie tree
    //     Get the length from the items in the tree
    //
    //     Note: the expression is not unique
    //      Both: "time#bell#" and "bell#time#" are fine
    //  Assumptions: no duplicate words
    //
    // Complexity: Time O(n), Space O(n)
    //    n = total count of characters in all words
    
    type TrieNode struct {
       is_leaf bool
       children map[byte]*TrieNode
    }
    
    func minimumLengthEncoding(words string) int {
        // build TrieTree
        res := 0
        leaf_count := 0
    
        root := TrieNode{children: make(map[byte]*TrieNode)}
        for _, word := range words {
            p := &root
            for i:=len(word)-1; i>=0; i-- {
                ch := word[i]
                q, status := p.children[ch]
                if status == false {
                    q = &TrieNode{children: make(map[byte]*TrieNode)}
                    p.children[ch] = q
                }
                p = q
                res += 1
                if p.is_leaf == true {
                    // revert
                    p.is_leaf = false
                    leaf_count -= 1
                    res -= (len(word) - i)
                }
            }
            p.is_leaf = true
            leaf_count += 1
            if len(p.children) != 0 {
                // revert
                p.is_leaf = false
                leaf_count -= 1
                res -= len(word)
            }
        }
        return res + leaf_count
    }