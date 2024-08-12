[[Keep/Colour/DEFAULT]] [[Keep/Archived]] 


class Solution:
    def nthFibonacci(self, n : int) -> int:
        # code here
        a = 1
        b = 1
        mod = 10**9 + 7
        if n <= 2: return b
        ct = 2
        while ct != n:
            temp = a
            a = b
            b = (temp+b)%mod
            ct += 1
        return b%mod
             






#{ 
 # Driver Code Starts
if __name__=="__main__":
    t = int(input())
    for _ in range(t):
        
        n = int(input())
        
        obj = Solution()
        res = obj.nthFibonacci(n)
        
        print(res)
        

# } Driver Code Ends
