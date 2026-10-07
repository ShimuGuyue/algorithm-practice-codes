

```cpp
void solve()
{
    int n, m;
    cin >> n >> m;
    for (int i = 1; i <= n; ++i)
    {
        cout << m / n + (i <= m % n ? 1 : 0) << '\n';
    }
}
```

