
```c++
static constexpr int64_t mod{ 998244353 };
std::vector<int64_t> factorials;
void init()
{
    int n{ 400000 };
    factorials.assign(n + 1, 1);
    for (int i = 2; i <= n; ++i)
    {
        factorials[i] = factorials[i - 1] * i % mod;
    }
}
```

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> as(n);
    std::vector<int> bs(n);
    for (auto& a : as)
    {
        std::cin >> a;
    }
    for (auto& b : bs)
    {
        std::cin >> b;
    }

    int min{ *std::min_element(bs.begin(), bs.end()) };
    int count{ std::count_if(as.begin(), as.end(), [min](int a){return a > min;}) };
    int64_t ans{ factorials[count] * factorials[n - count] % mod };
    std::cout << ans << '\n';
}
```

