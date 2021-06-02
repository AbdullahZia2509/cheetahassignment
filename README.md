# Cheetah Assignment
Each of the questions stated to only write the required function.
I'm adding all the functions to a single text file.

All of these questions are done using JAVA.

# Question 1 | lexicographical smallest string 

    static int MAX = 26;

    static String chooseAndSwap(String s, int n) {
        int i, j = 0;

        char[] str = s.toCharArray();

        int[] indexOfChar = new int[MAX];
        for (i = 0; i < MAX; i++)
            indexOfChar[i] = -1;

        for (i = 0; i < n; i++) {

            if (indexOfChar[str[i] - 'a'] == -1)
                indexOfChar[str[i] - 'a'] = i;
        }

        for (i = 0; i < n; i++) {
            boolean flag = false;

            for (j = 0; j < str[i] - 'a'; j++) {

                if (indexOfChar[j] > indexOfChar[str[i] - 'a']) {
                    flag = true;
                    break;
                }
            }

            if (flag)
                break;
        }

        if (i < n) {

            char ch1 = str[i];
            char ch2 = (char) (j + 'a');

            for (i = 0; i < n; i++) {

                if (str[i] == ch1)
                    str[i] = ch2;

                else if (str[i] == ch2)
                    str[i] = ch1;
            }
        }

        return String.valueOf(str);
    }


# Question 2 | Palindrome
    static int longestPalin(String str) {
        int n = str.length();

        int maxLength = 1, start = 0;

        for (int i = 0; i < str.length(); i++) {
            for (int j = i; j < str.length(); j++) {
                int flag = 1;

                for (int k = 0; k < (j - i + 1) / 2; k++)
                    if (str.charAt(i + k) != str.charAt(j - k)) {
                        flag = 0;
                        break;
                    }

                if (flag != 0 && (j - i + 1) > maxLength) {
                    start = i;
                    maxLength = j - i + 1;
                }
            }
        }

        System.out.print("Longest palindrome subString is: ");
        for (int i = start; i <= start + maxLength - 1; ++i)
            System.out.print(str.charAt(i));

        return maxLength;
    }
    
# Question 3 | Max Meetings
Question 3 takes two extra classes: a Java Comparator class which compares the meeting objects


      class mycomparator implements Comparator<meeting>
      {
          @Override
          public int compare(meeting o1, meeting o2)
          {
              if (o1.end < o2.end)
              {
                  return -1;
              }
              else if (o1.end > o2.end)
                  return 1;

              return 0;
          }
      }

      class meeting
      {
          int start;
          int end;
          int pos;

          meeting(int start, int end, int pos)
          {
              this.start = start;
              this.end = end;
              this.pos = pos;
          }
      }

      public static void maxMeeting(ArrayList<meeting> al, int s)
      {
          ArrayList<Integer> m = new ArrayList<>();

          int time_limit = 0;

          mycomparator mc = new mycomparator();

          Collections.sort(al, mc);

          m.add(al.get(0).pos);

          time_limit = al.get(0).end;

          for(int i = 1; i < al.size(); i++)
          {
              if (al.get(i).start > time_limit)
              {
                  m.add(al.get(i).pos);
                  time_limit = al.get(i).end;
              }
          }

           for(int i = 0; i < m.size(); i++)
              System.out.print(m.get(i) + 1 + " ");
      }
