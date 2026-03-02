

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> as(n);
    for (auto& a : as)
    {
        std::cin >> a;
    }

    for (auto a : as)
    {
        if (a == 1)
        {
            std::cout << "yes\n";
            return;
        }
        std::set<int> factors;
        for (int i = 2; i <= a; ++i)
        {
            if (a % i)
                continue;
            factors.insert(i);
            while (a % i == 0)
            {
                a /= i;
            }
        }
        if (factors.size() == 1)
        {
            std::cout << "yes\n";
            return;
        }
    }
    std::cout << "no\n";
}
```

