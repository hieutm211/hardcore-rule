<h1>PROBLEM 1 : Degree of an Array</h1>
//beats 93.85 % of cpp submissions. <br/><br/>

<code>
class Solution {
public:
    int ans, d[50004], first[50004], last[50004];

    template<class T> inline bool maximize(T& a, const T& b){ return a < b ? a = b, 1 : 0; }
    template<class T> inline bool minimize(T& a, const T& b){ return a > b ? a = b, 1 : 0; }

    int findShortestSubArray(vector<int>& nums) {
        int dmax;

        for (auto& x : nums){
            ++d[x];
            first[x] = nums.size();
        }

        dmax = 0;
        for (int i = 0; i < nums.size(); ++i){
            maximize(dmax, d[nums[i]]);
            minimize(first[nums[i]], i);
            maximize(last[nums[i]], i);
        }

        ans = nums.size();
        for (auto& x : nums) if (d[x] == dmax) minimize(ans, last[x]-first[x]+1);

        return ans;
    }
};
</code>

<h1>PROBLEM 2: 01 Matrix </h1> 
//beats 88.30 % of cpp submissions. <br/><br/>
	
<code>
class Solution {
public:
    queue<int> q;
    int n, m, dist[10005];    
    bool visited[10005];
    
    const int px[4] = {-1, 0, 1, 0};
    const int py[4] = {0, -1, 0, 1};
    
    int cell(int i, int j){ return i*m+j; }

    vector<vector<int>> updateMatrix(vector<vector<int>>& matrix){
        int cur, nxt, x, y, u, v;
            
        n = matrix.size();
        if (n != 0) m = matrix[0].size();
        
        for (int i = 0; i < n; ++i)
        for (int j = 0; j < m; ++j) 
            if (matrix[i][j] == 0){
                q.push(cell(i, j));
                visited[cell(i,j)] = 1;   
            }
        
        while (!q.empty()){
            cur = q.front(); q.pop();
            
            y = cur % m;
            x = (cur - y) / m;
            
            for (int i = 0; i < 4; ++i){
                u = x + px[i];
                v = y + py[i];
                nxt = cell(u, v);
                if (u < 0 || n-1 < u || v < 0 || m-1 < v) continue;
                if (!visited[nxt]){
                    visited[nxt] = 1;
                    dist[nxt] = dist[cur] + 1;
                    q.push(nxt);
                }
            }
        }
       
        for (int i = 0; i < n; ++i) 
        for (int j = 0; j < m; ++j) 
            matrix[i][j] = dist[cell(i, j)];
        
        return matrix;
    }
};
</code>

<h1>PROBLEM 3 : Rotate Image </h1><br/>

<code>
class Solution {                                                                    
public:                                                                             
    void rotate(vector<vector<int>>& matrix){                                       
        int n = matrix.size();                                                      
        for (int i = 0; i < n; ++i){                                               
            for (int k = 1; k < n-i; ++k) swap(matrix[i][i+k], matrix[i+k][i]);    
            reverse(matrix[i].begin(), matrix[i].end());                            
        }                                                                           
    }                                                                               
};                                                                                  
</code>

<h1>PROBLEM BONUS: Count of Smaller Numbers After Self </h1>
//beats 71.53 % of cpp submissions. <br/><br/>

<code>
class Solution {
public:
    int n, t[100005];
    vector<int> ans;    
    vector<pair<int, int> > tmp;

	void roirac(vector<int>& nums){
    	for (int i = 0; i < nums.size(); ++i) tmp.push_back({nums[i], i});
    	sort(tmp.begin(), tmp.end());

    	if (nums.size()) nums[tmp[0].second] = 1;
    	for (int i = 1; i < nums.size(); ++i)
        	nums[tmp[i].second] = nums[tmp[i-1].second] + (tmp[i].first != tmp[i-1].first);
	}
    
    inline void update(int i, int x){ for (; i < n+1; i += i & -i) t[i] += x; }
    inline int get(int i){
        int ans = 0;
        for (; i > 0; i -= i & -i) ans += t[i];
        return ans;
    }
    
    vector<int> countSmaller(vector<int>& nums) {
        n = nums.size();

        for (int i = 0; i < n; ++i) ans.push_back(0);
        
        roirac(nums);

        for (int i = n-1; i >= 0; --i){
            ans[i] = get(nums[i]-1);
            update(nums[i], 1);
        }

        return ans;
    }
};
</code>
