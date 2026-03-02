

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::map<int, int> m;
    std::vector<int> as(n);
    for (auto& a : as)
    {
        std::cin >> a;
    }
    for (auto a : as)
    {
        int b{ a };

        for (int i = 2; i * i <= b; ++i)
        {
            if (b % i)
                continue;
            if (m[i] != 0)
            {
                std::cout << m[i] << ' ' << a << '\n';
                return;
            }
            m[i] = a;
            while (b % i == 0)
            {
                b /= i;
            }
        }
        if (b != 1)
        {
            if (m[b] != 0)
            {
                std::cout << m[b] << ' ' << a << '\n';
                return;
            }
            m[b] = a;
        }
    }
    std::cout << -1 << '\n';
}
```

