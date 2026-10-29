

```cpp
void solve()
{
    int n, m;
    cin >> n >> m;
    vector<vector<int64_t>> grid(n, vector<int64_t>(m));
    for (auto& v : grid)
    {
        for (auto& a : v)
        {
            cin >> a;
        }
    }

    int64_t ans = 0;
    vector<vector<int64_t>> remains(n, vector<int64_t>(m));
    for (int i = 0; i < n; ++i)
    {
        for (int j = 0; j < m; ++j)
        {
            if (remains[i][j] < grid[i][j])
            {
                ans += grid[i][j] - remains[i][j];
                remains[i][j] = grid[i][j];
                if (j + 1 != m)
                    remains[i][j + 1] += remains[i][j];
                else
                    if (i + 1 != n)
                        remains[i + 1][j] += remains[i][j] - grid[i][j];
            }
            else
            {
                if (j + 1 != m)
                {
                    remains[i][j + 1] += grid[i][j];
                    if (i + 1 != n)
                        remains[i + 1][j] += remains[i][j] - grid[i][j];
                }
                else
                {
                    if (i + 1 != n)
                        remains[i + 1][j] += remains[i][j] - grid[i][j];
                }
            }
        }
    }
    cout << ans << '\n';
}
```

