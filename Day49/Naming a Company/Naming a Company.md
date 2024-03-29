# 2306. Naming a Company

You are given an array of strings ideas that represents a list of names to be used in the process of naming a company. The process of naming a company is as follows:

Choose 2 **distinct** names from `ideas`, call them `ideaA` and `ideaB`.

Swap the first letters of `ideaA` and `ideaB` with each other.

If **both** of the new names are not found in the original ideas, then the name ideaA ideaB (the **concatenation** of `ideaA` and `ideaB`, separated by a space) is a valid company name.

Otherwise, it is not a valid name.

Return the number of **distinct** valid names for the company.

**Example 1:**
```
Input: ideas = ["coffee","donuts","time","toffee"]
Output: 6
Explanation: The following selections are valid:
- ("coffee", "donuts"): The company name created is "doffee conuts".
- ("donuts", "coffee"): The company name created is "conuts doffee".
- ("donuts", "time"): The company name created is "tonuts dime".
- ("donuts", "toffee"): The company name created is "tonuts doffee".
- ("time", "donuts"): The company name created is "dime tonuts".
- ("toffee", "donuts"): The company name created is "doffee tonuts".
Therefore, there are a total of 6 distinct company names.

The following are some examples of invalid selections:
- ("coffee", "time"): The name "toffee" formed after swapping already exists in the original array.
- ("time", "toffee"): Both names are still the same after swapping and exist in the original array.
- ("coffee", "toffee"): Both names formed after swapping already exist in the original array.
```
**Example 2:**
```
Input: ideas = ["lack","back"]
Output: 0
Explanation: There are no valid selections. Therefore, 0 is returned.
``` 

**Constraints:**

* `2 <= ideas.length <= 5 * 104`
* `1 <= ideas[i].length <= 10`
* `ideas[i]` consists of lowercase English letters.
* All the strings in ideas are **unique**.

**Solution:**
```
class Solution {
    public long distinctNames(String[] ideas) {
        Set<String>[] suffByLetter = new Set[26];
        for(int i = 0; i < 26; i++) {
            suffByLetter[i] = new HashSet<>();
        }

        for(String idea : ideas) {
            suffByLetter[idea.charAt(0) - 'a'].add(idea.substring(1));
        }

        long pairs = 0;
        for(int i= 0; i < 26; i++) {
            for(int j= i + 1; j< 26; j++){
                int overlap = 0;
                for(String suffix : suffByLetter[i]) {
                    if(suffByLetter[j].contains(suffix)) {
                        overlap++;
                    }
                }

                pairs += (suffByLetter[i].size() - overlap) * (suffByLetter[j].size() - overlap) * 2;
            }
        }

        return pairs;
    }
}
```
