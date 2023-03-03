# Task2-Problem3

Longest Palindromic Substring:

Example 1:
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.

Example 2:
Input: s = "cbbd"
Output: "bb"


JavaScript:

var longestPalindrome = function (s) {
    
    let updatedString = getUpdatedString(s);
    
    const length = 2 * s.length + 1;
    let p = new Array(length);
    p.fill(0);
    let c = 0;
    let r = 0;
    let maxLength = 0;
    let position = -1;
    for (let i = 0; i < length; i++) {
        let mirror = 2 * c - i;
        if (i < r) {
            p[i] = Math.min(r - i, p[mirror]);
        }
        let a = i + (1 + p[i]);
        let b = i - (1 + p[i]);
        while (a < length && b >= 0 && updatedString[a] === updatedString[b]) {
            p[i]++;
            a++;
            b--;
        }
        if (i + p[i] > r) {
            c = i;
            r = i + p[i];
        }
        if (maxLength < p[i]) {
            maxLength = p[i];
            position = i;
        }
    }
    let offset = p[position];
    let result = "";
    for (let i = position - offset + 1; i <= position + offset - 1; i++) {
        if (updatedString[i] !== '#') {
            result += updatedString[i];
        }
    }
    return result;
};

function getUpdatedString(s) {
    let sb = "";
    for (let i = 0; i < s.length; i++) {
        sb += "#" + s[i];
    }
    sb += "#";
    return sb;
}
