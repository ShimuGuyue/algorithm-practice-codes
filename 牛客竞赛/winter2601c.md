

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int64_t> as(n);
    for (auto& a : as)
    {
        std::cin >> a;
    }

    int64_t ans{ *std::max_element(as.begin(), as.end()) * (n - 2) + as.front() + as.back() };
    std::cout << ans << '\n';
}
```

