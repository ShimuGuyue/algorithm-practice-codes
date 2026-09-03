

```cpp
struct Trie
{
    struct Node
    {
        int count{ 0 };
        std::array<int, 2> nexts{ };
    };
    int count{ 0 };
    std::vector<Node> trie{ std::vector<Node>(1) };

    void insert(std::string& s)
    {
        int node{ 0 };
        ++trie[0].count;
        for (char c : s)
        {
            int index{ c - '0' };
            if (trie[node].nexts[index] == 0)
            {
                trie[node].nexts[index] = trie.size();
                trie.emplace_back();
            }
            node = trie[node].nexts[index];
            ++trie[node].count;
            if (trie[node].count == 1)
                ++count;
        }
    }

    void erase(std::string& s)
    {
        int node{ 0 };
        --trie[0].count;
        for (char c : s)
        {
            int index{ c - '0' };
            node = trie[node].nexts[index];
            --trie[node].count;
            if (trie[node].count == 0)
                --count;
        }
    }
};
```

```cpp
void solve()
{
    int n;
    std::cin >> n;
    Trie trie;

    while (n--)
    {
        char op;
        std::string s;
        std::cin >> op >> s;
        if (op == '+')
            trie.insert(s);
        else
            trie.erase(s);
        std::cout << trie.count << '\n';
    }
}
```

