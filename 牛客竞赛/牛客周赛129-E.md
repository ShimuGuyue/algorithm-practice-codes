

```c++
void solve()
{
    constexpr int64_t mod{ 1000000007 };

    int n;
    std::cin >> n;

    auto quickpow = [mod](int64_t base, int64_t power)
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
    };

    std::vector<int64_t> factorials(n + 1);
    factorials[1] = 1;
    for (int i{ 2 }; i <= n; ++i)
    {
        factorials[i] = factorials[i - 1] * i % mod;
    }
    std::vector<int64_t> inv_factorials(n + 1);
    inv_factorials[n] = quickpow(factorials[n], mod - 2);
    for (int i{ n - 1 }; i >= 1; --i)
    {
        inv_factorials[i] = inv_factorials[i + 1] * (i + 1) % mod;
    }

    auto combinate = [&factorials, &inv_factorials, mod](int n, int k)
    {
        if (k == 0 || k == n)
            return INT64_C(1);
        return factorials[n] * inv_factorials[k] % mod * inv_factorials[n - k] % mod;
    };

    for (int k{ 1 }; k <= n; ++k)
    {
        std::cout << combinate(n, k) * quickpow(2, n - 1) % mod << ' ';
    }
    std::cout << '\n';
}
```

