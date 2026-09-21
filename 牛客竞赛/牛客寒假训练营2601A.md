

```c++
static constexpr int64_t mod{ 998244353 };

void solve()
{
    int c;
    std::cin >> c;
    std::array<int64_t, 8> ons;
    std::array<int64_t, 8> offs;
    for (int i = 1; i <= 7; ++i)
    {
        int p;
        std::cin >> p;
        ons[i] = p * inv(100) % mod;
        offs[i] = (100 - p) * inv(100) % mod;
    }

    std::array<int, 10> flags;
    flags[0] = ons[1] * ons[2] % mod * ons[3] % mod * offs[4] % mod * ons[5] % mod * ons[6] % mod * ons[7] % mod;
    flags[1] = offs[1] * offs[2] % mod * ons[3] % mod * offs[4] % mod * offs[5] % mod * ons[6] % mod * offs[7] % mod;
    flags[2] = ons[1] * offs[2] % mod * ons[3] % mod * ons[4] % mod * ons[5] % mod * offs[6] % mod * ons[7] % mod;
    flags[3] = ons[1] * offs[2] % mod * ons[3] % mod * ons[4] % mod * offs[5] % mod * ons[6] % mod * ons[7] % mod;
    flags[4] = offs[1] * ons[2] % mod * ons[3] % mod * ons[4] % mod * offs[5] % mod * ons[6] % mod * offs[7] % mod;
    flags[5] = ons[1] * ons[2] % mod * offs[3] % mod * ons[4] % mod * offs[5] % mod * ons[6] % mod * ons[7] % mod;
    flags[6] = ons[1] * ons[2] % mod * offs[3] % mod * ons[4] % mod * ons[5] % mod * ons[6] % mod * ons[7] % mod;
    flags[7] = ons[1] * offs[2] % mod * ons[3] % mod * offs[4] % mod * offs[5] % mod * ons[6] % mod * offs[7] % mod;
    flags[8] = ons[1] * ons[2] % mod * ons[3] % mod * ons[4] % mod * ons[5] % mod * ons[6] % mod * ons[7] % mod;
    flags[9] = ons[1] * ons[2] % mod * ons[3] % mod * ons[4] % mod * offs[5] % mod * ons[6] % mod * ons[7] % mod;

    int64_t ans{ 0 };
    for (int i = 0; i <= c; ++i)
    {
        int x{ i }, y{ c - i };
        std::array<int, 4> a;
        std::array<int, 4> b;
        for (int j = 0; j < 4; ++j)
        {
            a[j] = x % 10;
            x /= 10;
            b[j] = y % 10;
            y /= 10;
        }

        int64_t p{ 1 };
        for (int j = 0; j < 4; ++j)
        {
            p = p * flags[a[j]] % mod * flags[b[j]] % mod;
        }
        ans = (ans + p) % mod;
    }
    std::cout << ans << '\n';
}

int64_t quickpow(int64_t base, int64_t power)
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

int64_t inv(int64_t n)
{
    return quickpow(n, mod - 2);
}
```

