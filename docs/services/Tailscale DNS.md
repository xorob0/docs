Type: Cloud
Replaces: Nebula
Tags: VPN, Mesh, DNS, TLS

Config:
```
{
	"tagOwners": {
		"tag:admin":  ["xorob0@github"],
		"tag:server": ["xorob0@github"],
	},
	"acls": [
		{"action": "accept", "users": ["*"], "ports": ["*:*"]},
	],
	"ssh": [
		{
			"action": "accept",
			"src":    ["xorob0@github"],
			"dst":    ["tag:server"],
			"users":  ["root", "autogroup:nonroot"],
		},
		{
			"action": "accept",
			"src":    ["tag:server"],
			"dst":    ["tag:server"],
			"users":  ["root", "autogroup:nonroot"],
		},
	],
}
```
