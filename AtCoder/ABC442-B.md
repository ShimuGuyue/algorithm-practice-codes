

```c++
void solve()
{
    int q;
    std::cin >> q;
    int a{ 0 };
    bool b{ false };
    while (q--)
    {
        int x;
        std::cin >> x;
        if (x == 1)
            ++a;
        if (x == 2)
            a = a == 0 ? 0 : a - 1;
        if (x == 3)
            b = !b;
        if (a >= 3 && b)
            std::cout << "Yes\n";
        else
            std::cout << "No\n";
    }
}
```

