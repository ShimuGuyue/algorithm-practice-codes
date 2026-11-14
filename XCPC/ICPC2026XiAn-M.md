

```cpp
void solve()
{
    int n;
    cin >> n;
    array<string, 4> ss;
    for (auto& s : ss)
    {
        cin >> s;
    }

    vector<int> counts(4);
    vector<int> sums(4, 2000);
    vector<bool> zeros(4);
    for (int j = 0; j < n; ++j)
    {
        for (int i = 0; i < 4; ++i)
        {
            if (ss[i][j] == 'H')
                ++counts[i];
            else
                counts[i] = 0;

            if (counts[i] == 100)
            {
                for (int k = 0; k < 4; ++k)
                {
                    if (k != i)
                        sums[k] += 30;
                }
                counts[i] = 0;
            }

            if (ss[i][j] == 'J')
                sums[i] -= 50;
            else if (ss[i][j] == 'A')
                sums[i] -= 100;
            else if (ss[i][j] == 'M')
                sums[i] -= 200;

        }
        for (int i = 0; i < 4; ++i)
        {
            if (sums[i] > 2000)
                sums[i] = 2000;
            if (sums[i] <= 0)
                zeros[i] = true;
        }
    }

    for (int i = 0; i < 4; ++i)
    {
        if (zeros[i] == true)
            cout << 0 << ' ';
        else
            cout << sums[i] << ' ';
    }
    cout << '\n';
}
```

