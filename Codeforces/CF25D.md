

```cpp
class DisjointSet
{
private:
    struct Data
    {
        int father;
        int size;
    };
    std::vector<Data> nodes_;

    int count_;

public:
    DisjointSet(const int n)
    {
        build(n);
    }

public:
    int find(const int x)
    {
        return nodes_[x].father == x ? x : nodes_[x].father = find(nodes_[x].father);
    }

    void merge(const int x, const int y)
    {
        const int set_x{ find(x) };
        const int set_y{ find(y) };
        if (set_x == set_y)
            return;
        nodes_[set_y].father = set_x;
        nodes_[set_x].size += nodes_[set_y].size;
        --count_;
    }

    int count() const
    {
        return count_;
    }

    int get_size(const int x)
    {
        return nodes_[find(x)].size;
    }

private:
    void build(const int n)
    {
        count_ = n;

        nodes_.assign(n, { });
        for (int i{ 0 }; i < n; ++i)
        {
            nodes_[i].father = i;
            nodes_[i].size = 1;
        }
    }
};
```

```cpp
void solve()
{
    int n;
    std::cin >> n;

    DisjointSet ds(n + 1);

    std::vector<std::pair<int, int>> edges;
    for (int i{ 1 }; i < n; ++i)
    {
        int u, v;
        std::cin >> u >> v;
        if (ds.find(u) == ds.find(v))
            edges.push_back({u, v});
        else
            ds.merge(u, v);
    }
    std::vector<int> nodes;
    for (int i{ 1 }; i <= n; ++i)
    {
        nodes.push_back(ds.find(i));
    }
    std::sort(nodes.begin(), nodes.end());
    nodes.erase(std::unique(nodes.begin(), nodes.end()), nodes.end());
    std::cout << edges.size() << '\n';
    for (int i{ 0 }; i < edges.size(); ++i)
    {
        std::cout << edges[i].first << ' ' << edges[i].second << ' ';
        std::cout << nodes[i] << ' ' << nodes[i + 1] << '\n';
    }
}
```

