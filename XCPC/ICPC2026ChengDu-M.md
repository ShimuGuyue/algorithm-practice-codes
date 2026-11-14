

```cpp
void solve()
{
    int n;
    cin >> n;
    vector<pair<int, int>> lrs(n + 1);
    for (int i = 1; i <= n; ++i)
    {
        cin >> lrs[i].first >> lrs[i].second;
    }

    stack<int> k;
    k.push(lrs[n].first);
    for (int i = n - 1; i > 0; --i)
    {
        auto [l, r] = lrs[i];
        while (!k.empty() && r >= k.top())
        {
            l = std::max(l, k.top());
            k.pop();
        }
        k.push(l);
    }

    int ans = k.size();
    cout << ans << '\n';
}
```

