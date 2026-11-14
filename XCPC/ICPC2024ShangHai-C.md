

```cpp
void solve()
{
	int l, r;
	cin >> l >> r;
	int len = r - l + 1;
	if (l & 1)
	{
		if (len % 2 == 1)
		{
			cout << "Alice\n";
			return;
		}
		if (l * 2 <= r)
			cout << "Alice\n";
		else
			cout << "Bob\n";
	}
	else
	{
		if (len % 2 == 0)
		{
			cout << "Bob\n";
			return;
		}
		if (l * 2 + 2 <= r)
			cout << "Bob\n";
		else
			cout << "Alice\n";
	}
}
```

