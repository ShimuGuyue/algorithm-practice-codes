

```c++
void solve()
{
    std::string a, b;
    std::cin >> a >> b;

    int a1{ 0 }, a2{ 0 }, b1{ 0 }, b2{ 0 };
    if (a.back() == '+')
    {
        a1 = std::stoi(std::string(a.begin(), a.end() - 1));
        a2 = 1;
    }
    else
    {
        a1 = std::stoi(a);
    }
    if (b.back() == '+')
    {
        b1 = std::stoi(std::string(b.begin(), b.end() - 1));
        b2 = 1;
    }
    else
    {
        b1 = std::stoi(b);
    }

    if (a1 > b1)
    {
        std::cout << "Yes\n";
        return;
    }
    if (a1 == b1 && a2 > b2)
    {
        std::cout << "Yes\n";
        return;
    }
    std::cout << "No\n";
}
```

