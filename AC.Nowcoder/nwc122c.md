

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int64_t> as(n);
    for (auto &a : as)
    {
        std::cin >> a;
    }

    int64_t ans{ std::accumulate(as.begin(), as.end(), INT64_C(0)) };

    int64_t max{ *std::max_element(as.begin(), as.end()) };
    int64_t min{ *std::min_element(as.begin(), as.end()) };
    ans = std::min(ans, max + (min * n));
    std::cout << ans << '\n';
}
```

