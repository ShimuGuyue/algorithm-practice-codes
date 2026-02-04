

```c++
void solve()
{
    int n, k;
    std::cin >> n >> k;
    std::vector<int> as(n);
    for (auto& a : as)
    {
        std::cin >> a;
    }

    std::queue<int> q;
    for (int i = n - 1; i >= 0; --i)
    {
        q.push(as[i]);
    }
    q.push(k);

    int ans{ -10000000 };
    for (int i = 0; i <= n; ++i)
    {
        ans = std::max(ans, q.front() + q.back());
        q.push(q.front());
        q.pop();
    }
    std::cout << ans << '\n';
}
```

