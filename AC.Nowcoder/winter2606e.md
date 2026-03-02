

```c++
class DisjointSet
{
private:
	struct Node
	{
		int parent;
		int rank;
        int size;
	};

	std::vector<Node> nodes;

public:
	DisjointSet(int n) : nodes(n)
	{
		for (int i = 0; i < n; ++i)
		{
			nodes[i] = {i, 1, 1};
		}
	}

public:
	int find(int x)
	{
		return (nodes[x].parent == x) ? x : (nodes[x].parent = find(nodes[x].parent));
	}

	void merge(int x, int y)
	{
		int set_x = find(x);
		int set_y = find(y);
		if (nodes[set_x].rank < nodes[set_y].rank)
		{
			nodes[set_x].parent = set_y;
            nodes[set_y].size += nodes[set_x].size;
		}
		else
		{
			nodes[set_y].parent = set_x;
            nodes[set_x].size += nodes[set_y].size;
			if (nodes[set_x].rank == nodes[set_y].rank)
				++nodes[set_x].rank;
		}
	}

    int get_size(int x)
    {
        return nodes[find(x)].size;
    }
};
```

```c++
void solve()
{
    int n, m, x, d;
    std::cin >> n >> m >> x >> d;
    std::vector<int> as(n + 1);
    for (int i{ 1 }; i <= n; ++i)
    {
        std::cin >> as[i];
    }
    std::vector<int> as_sort{ as };
    std::sort(as_sort.begin(), as_sort.end());

    std::vector<std::pair<int, int>> edges(m);
    for (auto& [u, v] : edges)
    {
        std::cin >> u >> v;
        if (as[u] > as[v])
            std::swap(u, v);
    }
    std::sort(edges.begin(), edges.end(),
        [&as](std::pair<int, int> a, std::pair<int, int> b)
        {
            return as[a.first] > as[b.first];
        }
    );

    std::vector<int> hs(x);
    for (auto& h : hs)
    {
        std::cin >> h;
    }
    hs.push_back(std::numeric_limits<int>::max());

    std::vector<int> anss(x);
    int ans{ 0 };
    int index{ 0 };
    DisjointSet ds(n + 1); 
    for (int i{ x - 1 }; i >= 0; --i)
    {
        if (d == 1)
        {
            auto rt{ std::upper_bound(as_sort.begin(), as_sort.end(), hs[i + 1]) };
            auto lt{ std::upper_bound(as_sort.begin(), as_sort.end(), hs[i]) };
            ans += rt - lt;
        }
        while (index < m && as[edges[index].first] > hs[i])
        {
            auto [u, v]{ edges[index++] };
            if (ds.find(u) == ds.find(v))
                continue;

            int size1{ ds.get_size(u) }, size2{ ds.get_size(v) };
            if (size1 >= d)
                --ans;
            if (size2 >= d)
                --ans;
            ds.merge(u, v);
            if (ds.get_size(u) >= d)
                ++ans;
        }
        anss[i] = ans;
    }
    for (auto a : anss)
    {
        std::cout << a << '\n';
    }
}
```

