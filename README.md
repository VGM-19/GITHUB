class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        for (int i = digits.size() - 1; i >= 0; --i) {
            ++digits[i];
            digits[i] %= 10;
            if (digits[i] != 0) return digits;
        }
        digits.insert(digits.begin(), 1);
        return digits;
    }
};
class Solution {
public:
    string addBinary(string a, string b) {
        string ans;
        int i = a.size() - 1, j = b.size() - 1;
        for (int carry = 0; i >= 0 || j >= 0 || carry; --i, --j) {
            carry += (i >= 0 ? a[i] - '0' : 0) + (j >= 0 ? b[j] - '0' : 0);
            ans.push_back((carry % 2) + '0');
            carry /= 2;
        }
        reverse(ans.begin(), ans.end());
        return ans;
    }
};
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> d;
        for (auto& s : strs) {
            string k = s;
            sort(k.begin(), k.end());
            d[k].emplace_back(s);
        }
        vector<vector<string>> ans;
        for (auto& [_, v] : d) ans.emplace_back(v);
        return ans;
    }
};
class Solution {
public:
    string countAndSay(int n) {
        string s = "1";
        while (--n) {
            string t = "";
            for (int i = 0; i < s.size();) {
                int j = i;
                while (j < s.size() && s[j] == s[i]) ++j;
                t += to_string(j - i);
                t += s[i];
                i = j;
            }
            s = t;
        }
        return s;
    }
};
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        vector<vector<bool>> row(9, vector<bool>(9, false));
        vector<vector<bool>> col(9, vector<bool>(9, false));
        vector<vector<bool>> sub(9, vector<bool>(9, false));
        for (int i = 0; i < 9; ++i) {
            for (int j = 0; j < 9; ++j) {
                char c = board[i][j];
                if (c == '.') continue;
                int num = c - '0' - 1;
                int k = i / 3 * 3 + j / 3;
                if (row[i][num] || col[j][num] || sub[k][num]) {
                    return false;
                }
                row[i][num] = true;
                col[j][num] = true;
                sub[k][num] = true;
            }
        }
        return true;
    }
};
class Solution {
public:
    string multiply(string num1, string num2) {
        if (num1 == "0" || num2 == "0") {
            return "0";
        }
        int m = num1.size(), n = num2.size();
        vector<int> arr(m + n);
        for (int i = m - 1; i >= 0; --i) {
            int a = num1[i] - '0';
            for (int j = n - 1; j >= 0; --j) {
                int b = num2[j] - '0';
                arr[i + j + 1] += a * b;
            }
        }
        for (int i = arr.size() - 1; i; --i) {
            arr[i - 1] += arr[i] / 10;
            arr[i] %= 10;
        }
        int i = arr[0] ? 0 : 1;
        string ans;
        for (; i < arr.size(); ++i) {
            ans += '0' + arr[i];
        }
        return ans;
    }
};
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int k = 0;
        for (int x : nums) {
            if (x != val) {
                nums[k++] = x;
            }
        }
        return k;
    }
};
class Solution {
private:
    vector<int> Next(string str) {
        vector<int> n(str.length());
        n[0] = -1;
        int i = 0, pre = -1;
        int len = str.length();
        while (i < len) {
            while (pre >= 0 && str[i] != str[pre])
                pre = n[pre];
            ++i, ++pre;
            if (i >= len)
                break;
            if (str[i] == str[pre])
                n[i] = n[pre];
            else
                n[i] = pre;
        }
        return n;
    }

public:
    int strStr(string haystack, string needle) {
        if (0 == needle.length())
            return 0;

        vector<int> n(Next(needle));

        int len = haystack.length() - needle.length() + 1;
        for (int i = 0; i < len; ++i) {
            int j = 0, k = i;
            while (j < needle.length() && k < haystack.length()) {
                if (haystack[k] != needle[j]) {
                    if (n[j] >= 0) {
                        j = n[j];
                        continue;
                    } else
                        break;
                }
                ++k, ++j;
            }
            if (j >= needle.length())
                return k - j;
        }

        return -1;
    }
};
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        for (int i = 0; i < n >> 1; ++i) {
            for (int j = 0; j < n; ++j) {
                swap(matrix[i][j], matrix[n - i - 1][j]);
            }
        }
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < i; ++j) {
                swap(matrix[i][j], matrix[j][i]);
            }
        }
    }
};
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if (!head || !head->next) {
            return head;
        }
        ListNode* t = swapPairs(head->next->next);
        ListNode* p = head->next;
        p->next = head;
        head->next = t;
        return p;
    }
};
class Solution {
public:
    int divide(int a, int b) {
        if (b == 1) {
            return a;
        }
        if (a == INT_MIN && b == -1) {
            return INT_MAX;
        }
        bool sign = (a > 0 && b > 0) || (a < 0 && b < 0);
        a = a > 0 ? -a : a;
        b = b > 0 ? -b : b;
        int ans = 0;
        while (a <= b) {
            int x = b;
            int cnt = 1;
            while (x >= (INT_MIN >> 1) && a <= (x << 1)) {
                x <<= 1;
                cnt <<= 1;
            }
            ans += cnt;
            a -= x;
        }
        return sign ? ans : -ans;
    }
};
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int n = nums.size();
        int i = n - 2;
        while (~i && nums[i] >= nums[i + 1]) {
            --i;
        }
        if (~i) {
            for (int j = n - 1; j > i; --j) {
                if (nums[j] > nums[i]) {
                    swap(nums[i], nums[j]);
                    break;
                }
            }
        }
        reverse(nums.begin() + i + 1, nums.end());
    }
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int l = 0, r = nums.size();
        while (l < r) {
            int mid = (l + r) >> 1;
            if (nums[mid] >= target) {
                r = mid;
            } else {
                l = mid + 1;
            }
        }
        return l;
    }
};
class Solution {
public:
    vector<int> twoSum(vector<int> &nums, int target) {
        for (int i = 0; i < nums.size(); i++) {
            for (int j = i + 1; j < nums.size(); j++) {
                if (nums[j] == target - nums[i]) {
                    return {i, j};
                }
            }
        }
        // Return an empty vector if no solution is found
        return {};
    }
};
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int cnt[128]{};
        int ans = 0, n = s.size();
        for (int l = 0, r = 0; r < n; ++r) {
            ++cnt[s[r]];
            while (cnt[s[r]] > 1) {
                --cnt[s[l++]];
            }
            ans = max(ans, r - l + 1);
        }
        return ans;
    }
};
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* ret = nullptr;
        ListNode* cur = nullptr;
        int carry = 0;
        while (l1 != nullptr || l2 != nullptr || carry != 0) {
            carry += (l1 == nullptr ? 0 : l1->val) + (l2 == nullptr ? 0 : l2->val);
            auto temp = new ListNode(carry % 10);
            carry /= 10;
            if (ret == nullptr) {
                ret = temp;
                cur = ret;
            }
            else {
                cur->next = temp;
                cur = cur->next;
            }
            l1 = l1 == nullptr ? nullptr : l1->next;
            l2 = l2 == nullptr ? nullptr : l2->next;
        }
        return ret;
    }
};
class Solution {
public:
    string longestPalindrome(string s) {
        int n = s.size();
        vector<vector<bool>> f(n, vector<bool>(n, true));
        int k = 0, mx = 1;
        for (int i = n - 2; ~i; --i) {
            for (int j = i + 1; j < n; ++j) {
                f[i][j] = false;
                if (s[i] == s[j]) {
                    f[i][j] = f[i + 1][j - 1];
                    if (f[i][j] && mx < j - i + 1) {
                        mx = j - i + 1;
                        k = i;
                    }
                }
            }
        }
        return s.substr(k, mx);
    }
};
class Solution {
public:
    string convert(string s, int numRows) {
        if (numRows == 1) {
            return s;
        }
        vector<string> g(numRows);
        int i = 0, k = -1;
        for (char c : s) {
            g[i] += c;
            if (i == 0 || i == numRows - 1) {
                k = -k;
            }
            i += k;
        }
        string ans;
        for (auto& t : g) {
            ans += t;
        }
        return ans;
    }
};
class Solution {
public:
    int reverse(int x) {
        int ans = 0;
        for (; x; x /= 10) {
            if (ans < INT_MIN / 10 || ans > INT_MAX / 10) {
                return 0;
            }
            ans = ans * 10 + x % 10;
        }
        return ans;
    }
};
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0 || (x && x % 10 == 0)) {
            return false;
        }
        int y = 0;
        for (; y < x; x /= 10) {
            y = y * 10 + x % 10;
        }
        return x == y || x == y / 10;
    }
};
class Solution {
public:
    int romanToInt(string s) {
        unordered_map<char, int> nums{
            {'I', 1},
            {'V', 5},
            {'X', 10},
            {'L', 50},
            {'C', 100},
            {'D', 500},
            {'M', 1000},
        };
        int ans = nums[s.back()];
        for (int i = 0; i < s.size() - 1; ++i) {
            int sign = nums[s[i]] < nums[s[i + 1]] ? -1 : 1;
            ans += sign * nums[s[i]];
        }
        return ans;
    }
};
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        int n = strs.size();
        for (int i = 0; i < strs[0].size(); ++i) {
            for (int j = 1; j < n; ++j) {
                if (strs[j].size() <= i || strs[j][i] != strs[0][i]) {
                    return strs[0].substr(0, i);
                }
            }
        }
        return strs[0];
    }
};
class Solution {
public:
    bool isValid(string s) {
        string stk;
        for (char c : s) {
            if (c == '(' || c == '{' || c == '[')
                stk.push_back(c);
            else if (stk.empty() || !match(stk.back(), c))
                return false;
            else
                stk.pop_back();
        }
        return stk.empty();
    }

    bool match(char l, char r) {
        return (l == '(' && r == ')') || (l == '[' && r == ']') || (l == '{' && r == '}');
    }
};
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        if (!list1) return list2;
        if (!list2) return list1;
        if (list1->val <= list2->val) {
            list1->next = mergeTwoLists(list1->next, list2);
            return list1;
        } else {
            list2->next = mergeTwoLists(list1, list2->next);
            return list2;
        }
    }
};
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int k = 0;
        for (int x : nums) {
            if (k == 0 || x != nums[k - 1]) {
                nums[k++] = x;
            }
        }
        return k;
    }
};
class Solution {
public:
    vector<int> twoSum(vector<int> &nums, int target) {
        for (int i = 0; i < nums.size(); i++) {
            for (int j = i + 1; j < nums.size(); j++) {
                if (nums[j] == target - nums[i]) {
                    return {i, j};
                }
            }
        }
        // Return an empty vector if no solution is found
        return {};
    }
};
#include <stdio.h>

int main() {
    float num1, num2, result;

    // Input two float values
    printf("Enter the first float value: ");
    scanf("%f", &num1);
    
    printf("Enter the second float value: ");
    scanf("%f", &num2);

    // Multiply the numbers
    result = num1 * num2;

    // Print the result up to 2 decimal places
    printf("The result of %.2f multiplied by %.2f is %.2f\n", num1, num2, result);

    return 0;
}
#include <stdio.h>

int main() {
    int num1, num2, sum;

    // Input two integers
    printf("Enter the first integer: ");
    scanf("%d", &num1);
    
    printf("Enter the second integer: ");
    scanf("%d", &num2);

    // Calculate the sum
    sum = num1 + num2;

    // Print the sum
    printf("The sum of %d and %d is %d\n", num1, num2, sum);

    return 0;
}


