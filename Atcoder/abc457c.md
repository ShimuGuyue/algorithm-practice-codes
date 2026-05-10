

```cpp
void solve()
{
    int64_t n, k;
    std::cin >> n >> k;
    std::vector<std::vector<int>> as(n);
    for (auto& v : as)
    {
        int m;
        std::cin >> m;
        v.resize(m);
        for (auto& a : v)
        {
            std::cin >> a;
        }
    }
    std::vector<int64_t> cs(n);
    for (auto& c : cs)
    {
        std::cin >> c;
    }

    int64_t sum{ 0 };
    for (int i{ 0 }; i < n; ++i)
    {
        int m{ int(as[i].size()) };
        int64_t cur{ cs[i] * m };
        if (k > sum + cur)
        {
            sum += cur;
            continue;
        }
        k -= sum;
        --k;
        k %= m;
        std::cout << as[i][k] << '\n';
        break;
    }
}
```

