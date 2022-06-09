6 月算法集训第二天

题目2278

```java
    class Solution {
        public int percentageLetter(String s, char letter) {
            int i,count = 0;
            for(i = 0; i < s.length();++i){
                if(s.charAt(i) == letter){
                    ++count;
                }
            }          
            return (int) Math.floor(100 * count / s.length() );
        }
    } 
```





题目 551

```java
class Solution {
    public boolean checkRecord(String s) {

        int i,j,count = 0;
        for(i =0; i < s.length(); ++i){
            if(s.charAt( i )=='A'){
                count++;
                if(count == 2){
                    return false;
                }
            }
            if( i + 2 < s.length()){
                if(s.charAt(i) == 'L' && s.charAt(i+1)=='L' && s.charAt(i+2) == 'L'){
                    return false;
                }
            }
        }
        return true;

    }
}
```

题目 2255

```java
class Solution {
    public int countPrefixes(String[] words, String s) {
        HashSet<String> set = new HashSet<>();
        int i,count = 0;
        for(i = 1; i <= s.length(); i++){
            set.add(s.substring( 0, i));
        }
        for(i = 0; i < words.length; i++){
            if(set.contains( words[i] )){
                ++count;
            }
        }
        return count;
    }
}
```

题目1071

```java
未解决明天搞
```

