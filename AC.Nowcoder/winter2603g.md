

```c++
void solve()
{
    int n, m;
    std::cin >> n >> m;
    std::vector<int64_t> as(n);
    std::vector<int64_t> bs(m);
    for (auto& a : as)
    {
        std::cin >> a;
    }
    for (auto& b : bs)
    {
        std::cin >> b;
    }

    int64_t sum_a{ std::accumulate(as.begin(), as.end(), INT64_C(0)) };
    int64_t sum_b{ std::accumulate(bs.begin(), bs.end(), INT64_C(0)) };
    if (sum_a == sum_b)
    {
        std::cout << 1 << '\n';
        return;
    }

    std::sort(as.begin(), as.end());
    std::sort(bs.begin(), bs.end());

    int ans{ 0 };
    if (sum_a > sum_b)
    {
        while (sum_a > sum_b)
        {
            ++ans;
            sum_a -= as.back();
            as.pop_back();
        }
    }
    else
    {
        while (sum_b > sum_a)
        {
            ++ans;
            sum_b -= bs.back();
            bs.pop_back();
        }
    }
    std::cout << ans << '\n';
}
```

