

```c++
void solve()
{
    int n, p, k;
    std::cin >> n >> p >> k;
    std::map<std::string, int64_t> counts;
    for (int i = 0; i < n; ++i)
    {
        std::string s;
        int count;
        std::cin >> s >> count;
        counts[s] = count;
    }

    std::vector<std::string> flags(k);
    for (auto& s : flags)
    {
        std::cin >> s;
    }

    if (p < k)
    {
        std::cout << -1 << '\n';
        return;
    }

    int64_t max_out{ INT64_MAX };
    for (auto& s : flags)
    {
        max_out = std::min(max_out, counts[s]);
    }

    int64_t sum{ 0 };
    for (auto& [k, v] : counts)
    {
        sum += v;
    }
    if (sum > p * max_out)
    {
        std::cout << -1 << '\n';
        return;
    }

    int64_t min_out{ (sum + p - 1) / p };
    std::cout << min_out << ' ' << max_out << '\n';
}
```

