# Leetcode-2429

# C++

class Solution {
public:
    int minimizeXor(int num1, int num2) {
        int count=0;
        while(num2)
        {
            if(num2&1)count++;
            num2=num2>>1;
        }
        vector<int>v;
        while(num1)
        {
            if(num1&1)v.push_back(1);
            else
            v.push_back(0);
            num1=num1>>1;
        }
        int k;
        if(v.size()>count)k=v.size();
        else
        k=count;
        vector<int>a(k,0);
        for(int i=v.size()-1;i>=0;i--)
        {
            if(v[i]==1&&count)
            {
                a[i]=1;
                count--;
            }
        }
        if(count)
        {
            for(int i=0;i<a.size();i++)
            {
                if(a[i]==0&&count)
                {
                    a[i]=1;
                    count--;
                }
                //cout<<i<<"\n";
            }
        }
        int ans=0;
        for(int i=a.size()-1;i>=0;i--)
        {
            ans=ans<<1;
            ans+=a[i];
        }
        return ans;
    }
};


# Java

import java.util.ArrayList;

class Solution {
    public int minimizeXor(int num1, int num2) {
        // Count the number of 1s in num2
        int count = 0;
        while (num2 != 0) {
            if ((num2 & 1) == 1) {
                count++;
            }
            num2 >>= 1;
        }

        // Convert num1 to binary representation in reverse order
        ArrayList<Integer> v = new ArrayList<>();
        while (num1 != 0) {
            if ((num1 & 1) == 1) {
                v.add(1);
            } else {
                v.add(0);
            }
            num1 >>= 1;
        }

        // Determine the size of the result array
        int k = Math.max(v.size(), count);
        int[] a = new int[k];

        // Assign 1s from v to a as long as count allows
        for (int i = v.size() - 1; i >= 0; i--) {
            if (v.get(i) == 1 && count > 0) {
                a[i] = 1;
                count--;
            }
        }

        // Assign remaining 1s to the leftmost available positions in a
        if (count > 0) {
            for (int i = 0; i < a.length; i++) {
                if (a[i] == 0 && count > 0) {
                    a[i] = 1;
                    count--;
                }
            }
        }

        // Calculate the final result from binary representation in a
        int ans = 0;
        for (int i = a.length - 1; i >= 0; i--) {
            ans = (ans << 1) | a[i];
        }

        return ans;
    }
}


# Python

class Solution:
    def minimizeXor(self, num1: int, num2: int) -> int:
        # Count the number of 1s in num2
        count = 0
        while num2:
            if num2 & 1:
                count += 1
            num2 >>= 1

        # Convert num1 to binary representation in reverse order
        v = []
        while num1:
            if num1 & 1:
                v.append(1)
            else:
                v.append(0)
            num1 >>= 1

        # Determine the size of the result vector
        k = max(len(v), count)
        a = [0] * k

        # Assign 1s from v to a as long as count allows
        for i in range(len(v) - 1, -1, -1):
            if v[i] == 1 and count:
                a[i] = 1
                count -= 1

        # Assign remaining 1s to the leftmost available positions in a
        if count:
            for i in range(len(a)):
                if a[i] == 0 and count:
                    a[i] = 1
                    count -= 1

        # Calculate the final result from binary representation in a
        ans = 0
        for i in range(len(a) - 1, -1, -1):
            ans = (ans << 1) | a[i]

        return ans
