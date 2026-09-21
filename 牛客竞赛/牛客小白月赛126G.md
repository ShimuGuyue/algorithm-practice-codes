

```c++
void solve()
{
    int n, q;
    std::cin >> n >> q;

    std::vector<int> dif_difs(n + 3);
    std::vector<int> difs(n + 3);
    std::vector<int64_t> as(n + 3);
    for (int i = 0; i < n; ++i)
    {
        int a, b;
        std::cin >> a >> b;
        if (b - a > 3)
        {
            int l{ (a + b) / 2 };
            int r{ l + 1 };
            ++dif_difs[a + 2];
            --dif_difs[l + 1];
            --dif_difs[r + 1];
            ++dif_difs[b];

            difs[l + 1] -= l - a - 1;
            difs[r] += b - r - 1;
        }
        if (a - 1 > 1)
        {
            --dif_difs[2];
            ++dif_difs[a];

            difs[1] += a - 2;
        }
        ++dif_difs[b + 2];
    }

    int presum{ 0 };
    for (int i = 1; i <= n; ++i)
    {
        presum += dif_difs[i];
        difs[i] += presum;
    }
    std::partial_sum(difs.begin(), difs.end(), as.begin());

    while (q--)
    {
        int x;
        std::cin >> x;
        std::cout << as[x] << ' ';
    }
    std::cout << '\n';
}
```

