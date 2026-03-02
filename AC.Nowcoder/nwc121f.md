

```c++
void solve()
{
    int n, q;
    std::cin >> n >> q;
    std::vector<int> as(n + 1);
    for (int i = 1; i <= n; ++i)
    {
        std::cin >> as[i];
        as[i] = turn(as[i]);
    }

    while (q--)
    {
        int l, r;
        std::cin >> l >> r;
        // 最多26个质数选不出完全平方数乘积
        if (r - l + 1 > 25)
        {
            std::cout << "Yes\n";
            continue;
        }
        // 异或线性基
        struct XorBasis
        {
            std::array<int, 25> basiss{};
            bool zeroflag{ false };

            void insert(int x)
            {
                if (x == 0)
                {
                    zeroflag = true;
                    return;
                }
                for (int i = 24; i >= 0; --i)
                {
                    if (x >> i & 1)
                    {
                        if (basiss[i] == 0)
                        {
                            basiss[i] = x;
                            return;
                        }
                        x ^= basiss[i];
                    }
                }
                zeroflag = true;
            }
        } xorBasis;

        for (int i = l; i <= r; ++i)
        {
            xorBasis.insert(as[i]);
        }
        std::cout << (xorBasis.zeroflag ? "Yes" : "No") << '\n';
    }
}

int turn(int n)
{
    static std::array<int, 25> primes{
        2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97
    };

    int ans{};
    for (int i = 0; i < 25; ++i)
    {
        while (n % primes[i] == 0)
        {
            n /= primes[i];
            ans ^= 1 << i;
        }
    }
    return ans;
}
```

