

```c++
static constexpr int64_t mod{ 1000000007 };

void solve()
{   // 打表找规律
    int n;
    std::cin >> n;

    int power{ n / 2 };
    int64_t ans{ quick_pow(2, power) };
    std::cout << ans << '\n';
}

int64_t quick_pow(int64_t base, int64_t n)
{
    int64_t ans{ 1 };
    while (n)
    {
        if (n & 1)
            ans = ans * base % mod;
        base = base * base % mod;
        n /= 2;
    }
    return ans;
}
```

