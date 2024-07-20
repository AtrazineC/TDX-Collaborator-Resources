# New Map Format
This guide will go over how to format a map properly for TDX.

# Checks
Before we begin, ensure the following on your map.

## 1. Lighting `ClockTime`
`ClockTime` MUST be a positive number. It won't work if it is negative.

![image](https://github.com/user-attachments/assets/ebbe7161-b87d-442d-a8d8-3a9cc6622fd1)

## 2. Custom materials in `MaterialService`
Your map might use custom materials like this:

![image](https://github.com/user-attachments/assets/0575a9c7-a6f0-41cd-9243-06c6034991f8)

If this is the case, we must rename these materials in order to not conflict with other maps with custom materials. Run the below script in the Command Bar, replacing `YOUR_MAP_NAME` with the name of the map:
```lua
local MAP_NAME = "YOUR_MAP_NAME"

local MaterialService = game:GetService("MaterialService")

for _, Material: MaterialVariant in pairs(MaterialService:GetChildren()) do
	Material.Name = MAP_NAME .. "_" .. Material.Name
end

for _, BasePart: BasePart in pairs(workspace:GetDescendants()) do
	if BasePart:IsA("BasePart") then
		if BasePart.MaterialVariant ~= "" then
			BasePart.MaterialVariant = MAP_NAME .. "_" .. BasePart.MaterialVariant
		end
	end
end
```

Now, your materials under `MaterialService` should look something like this for example:

![image](https://github.com/user-attachments/assets/d2b5a1a4-1661-4b21-9a4d-428bd98aa581)

# Template
- Template download (Discord): https://discord.com/channels/1071945224579973160/1165740168473489519/1264288052277284874
- Example map download (Discord): https://discord.com/channels/1071945224579973160/1165740168473489519/1264287561095057450

Here is what the template contains initially:

![image](https://github.com/user-attachments/assets/fc297952-e473-445a-8b01-7339fef3e1ff)

![image](https://github.com/user-attachments/assets/01e7406a-718c-4d35-8713-5a383c0f3d16)

## 1. LightingEffects
- Place all effects in Lighting such as `Sky`, `Bloom`, etc. instances in LightingEffects. 

