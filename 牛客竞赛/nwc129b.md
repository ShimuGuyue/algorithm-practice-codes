

```c++
void solve()
{
    std::string s;
    std::cin >> s;
    std::string t{ s };
    std::reverse(t.begin(), t.end());
    if (s > t)
        std::cout << "left\n";
    if (s == t)
        std::cout << "equal\n";
    if (s < t)
        std::cout << "right\n";
}
```

