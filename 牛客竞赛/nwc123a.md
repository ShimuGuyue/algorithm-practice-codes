

```c++
void solve()
{
    int a;
    char b;
    int c;
    char d;
    std::cin >> a >> b;
    std::cin >> c >> d;

    if (a > c || (a == c && b < d))
    {
        std::cout << "Yes\n";
        return;
    }
    std::cout << "No\n";
}
```

