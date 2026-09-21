

```c++
static constexpr int64_t mod{ 1000000007 };
std::vector<int64_t> factorials;
std::vector<int64_t> inv_factorials;

void init()
{
    constexpr int n{ 200000 };
    factorials.assign(n + 1, 1);
    for (int i = 2; i <= n; ++i)
    {
        factorials[i] = factorials[i - 1] * i % mod;
    }
    inv_factorials.assign(n + 1, 1);
    inv_factorials[n] = quickpow(factorials[n], mod - 2);
    for (int i = n - 1; i > 0; --i)
    {
        inv_factorials[i] = inv_factorials[i + 1] * (i + 1) % mod;
    }
}

int64_t quickpow(int64_t base, int power)
{
    int64_t ans{ 1 };
    while (power)
    {
        if (power & 1)
            ans = ans * base % mod;
        base = base * base % mod;
        power /= 2;
    }
    return ans;
}
```

```c++
void solve()
{
    int64_t n, m;
    std::cin >> n >> m;
    std::map<int, int64_t> counts;
    for (int i = 0; i < n; ++i)
    {
        int a;
        std::cin >> a;
        ++counts[a];
    }

    int64_t count{ 0 };
    for (auto [k, v] : counts)
    {
        if (v % k)
        {
            std::cout << 0 << '\n';
            return;
        }
        count += v / k;
    }
    if (count > m)
    {
        std::cout << 0 << '\n';
        return;
    }

    int64_t ans{ 1 };
    for (auto [k, v] : counts)
    {
        ans = ans * inv_factorials[v / k] % mod;
        while (v)
        {
            ans = ans * combinate(v, k) % mod;
            v -= k;
        }
    }
    for (int i = 0; i < count; ++i)
    {
        ans = ans * (m - i) % mod;
    }
    std::cout << ans << '\n';
}

int64_t combinate(int n, int k)
{
    if (k == 0 || k > n)
        return 0;
    return factorials[n] * inv_factorials[k] % mod * inv_factorials[n - k] % mod;
}
```

