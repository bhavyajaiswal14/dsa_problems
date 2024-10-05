# dsa_problems
<!--❓ ...
- ... <br>
- Optimization : ...
<details>
<summary>Optimal code</summary>
  
```cpp []
  code
```
</details>
-->

❓ Divide Players Into Teams of Equal Skill - 2491
- LC_Array_M_60_32_`Sort&2Pointer&PairSmallestw/Largest`_04102024<br>
- Optimization : `Frequency array`  
<details>
<summary>Optimal code</summary>
  
```cpp []
   long long dividePlayers(vector<int>& skill) {

        int max_skill = 1000;  // Max individual skill value
        vector<int> freq(max_skill + 1, 0); // Precise space allocation
        int teams = skill.size(); // Total players
        long long totalsum = 0;

        // Populate freq. array and total sum of skill[]
        for (int s : skill) {
            totalsum += s; 
            freq[s]++;
        }

        teams >>= 1;  // Bitwise division (total player/2)
        if (totalsum % teams != 0) return -1;  // Total skill cannot be divided equally pairwise.

        int target_pair_skill = totalsum / teams;
        int indv_skill_req = target_pair_skill/2;
        long long chemistry = 0;

        for (int i = 0; i <= indv_skill_req; ++i) {

            if (freq[i] == 0) continue;  // Skip if no players with this skill
            int partner_skill = target_pair_skill - i; // If player preset find partner

            // Case : For player and partner diff. skill 
            if (i != partner_skill) {

                // If both skill not present pair cannot be formed
                if (freq[i] != freq[partner_skill]) return -1;

                // player_skill * partner_skill * freq        
                chemistry += 1LL * i * partner_skill * freq[i];

                freq[partner_skill] = 0;  // Remove partner skill
            }

            // Case : If both partner and player have same skill
            else {
                 // freq[289]=2,4 to make pairs , 2 players with 289 skill
                if (freq[i] % 2 != 0) return -1;

                chemistry+= 1LL * i * i * (freq[i] / 2);
            }
            freq[i] = 0; // Remove player skill
        }

        return chemistry;
    }
```
</details><br>

❓ Permutation in String - 567
- LC_String_M_9_`SlidingWindow&FrequencyCount`_05102024 <br>
- Pattern : Apply sliding window when you need to find pattern/sum in a subarray/substring
<details>
<summary>Optimal code</summary>
  
```cpp []
        bool checkInclusion(string s1, string s2) {

        // If s1 is longer than s2, return false because s2 cannot contain s1
        if(s1.length()>s2.length()){
            return false;
        }

        // Step 1: Create two frequency arrays, one for s1 and one for the current window in s2
        vector<int>s1Count(26,0), sizeOfWin(26,0); // Size 26 for 'a' to 'z'

        // Step 2: Count the frequency of characters in s1 and in the first window of s2
        for(int i=0;i<s1.length();i++){
            s1Count[s1[i]-'a']++; // Frequency count for s1
            sizeOfWin[s2[i]-'a']++; // Initial window of s2

        }

        // Step 3: Slide the window over s2
        for(int i=s1.length();i<s2.length();i++){
            // Check if the current window matches the frequency of s1
            if(s1Count==sizeOfWin){
                return true; // If frequencies match, it means we found a permutation
            }

            // Slide the window: remove the character going out of the window (i - s1.length())
            sizeOfWin[s2[i-s1.length()]-'a']--;
            // Add the character coming into the window (i)
            sizeOfWin[s2[i]-'a']++;
        }

        // Step 4: After the loop, we need to check the last window
        return s1Count==sizeOfWin; // Check if the last window matches
    }
```
</details>
