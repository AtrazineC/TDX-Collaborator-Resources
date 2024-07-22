# New map format
- This guide will go over how to format a map properly for TDX
- Let me (Atrazine) know if you have any questions!

# General guidelines
- Ensure you're not doing too much with lighting effects such as saturation/contrast
- Try to name/group things to the best of your ability. Organization helps a lot!

# Checks
Before we begin, ensure the following on your map.

## 1. Lighting `ClockTime`
`ClockTime` MUST be a positive number. It won't work if it is negative.

![image](https://github.com/user-attachments/assets/ebbe7161-b87d-442d-a8d8-3a9cc6622fd1)

## 2. Collisions
- Make sure to turn off collisions for things like foiliage, small trees, etc.
- If your map contains holes the player can fall into, use an invisible part so that the player can't fall in and get stuck

## 3. Custom materials in `MaterialService`
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
- Template download (Discord): https://discord.com/channels/1071945224579973160/1165740168473489519/1264659080405057700
- Example of set up map (Discord): https://discord.com/channels/1071945224579973160/1165740168473489519/1264287561095057450

Here is what the template contains initially:

![image](https://github.com/user-attachments/assets/efb87bff-b7f5-4964-ab53-deb7ffd7bbad)

![image](https://github.com/user-attachments/assets/97e4274f-a0f7-43e0-bd1c-088636f0eda3)

## 1. Initial steps
- Place the map template into your `.rbxl` file containing your map
- Name the template the name of the map
- Put your name (preferably your Discord contact) in the Author `StringValue`. This is so I can contact you if there are issues

![image](https://github.com/user-attachments/assets/a57e0502-f216-44c0-b433-59633e4987ee)

![image](https://github.com/user-attachments/assets/3bbf316e-2386-4f38-bab9-724b951c1cde)

## 2. LOSIgnore
- Place objects/models that you don't want to affect tower's LOS here. For example, streetlights, thin trees, etc. should be placed here
- Objects placed in LOSIgnore will still be respected for placement. For example, if a house is in LOSIgnore, it will not block LOS of towers, but towers can't be placed inside the house

![image](https://github.com/user-attachments/assets/16bc7a41-3177-4e44-b588-7757f63c160c)

![image](https://github.com/user-attachments/assets/1da06256-c047-4a0e-82e7-e4db86405978)

## 3. RaycastIgnore
- Place objects/models that you don't want to affect tower placement or LOS of towers. For example, grass, small foiliage, etc.
- Invisible parts should also be placed here
- Essentially, any parts you don't want affecting tower placement should be placed here

![image](https://github.com/user-attachments/assets/f18ccba6-7aef-410e-9a1d-4abc55b6e890)

![image](https://github.com/user-attachments/assets/6d06c619-1129-41fd-8365-b668ff0cf1e9)

## 4. LightingEffects
- Place all effects in Lighting such as `Sky`, `Bloom`, etc. instances in LightingEffects. 

![image](https://github.com/user-attachments/assets/44abaff3-7ae6-455d-8482-226068bbbe40)

## 5. Zones

![image](https://github.com/user-attachments/assets/2ba3de15-cd21-4bd8-8e63-7cf11113fa34)

### 5.1 Path
- If the path is not composed of simple parts, we need to cover it with parts for the raycasting. This is because Roblox's raycasting is not accurate enough for mesh/union paths
- For example, in the map "Singularity," the path is a complex mesh, so these parts must be manually placed for collision purposes

![image](https://github.com/user-attachments/assets/a6ee8e38-b8a1-4471-95ab-ce365b3a6e5b)

- These parts should be placed inside the Path folder, and should be made invisible once complete

![image](https://github.com/user-attachments/assets/f0ab3510-5132-4157-8a34-9da910f11a2a)

- These manual parts are **NOT needed if the path is composed of simple parts**. If the path is composed of simple parts, check the `UsePathHighlight` box and leave the folder empty

![image](https://github.com/user-attachments/assets/38dcd4f9-fb03-4a02-b28b-fae31789ae3a)

### 5.2 Water
- If your map contains water that is a regular Roblox part, place those parts inside the Water folder
- If your map doesn't use Roblox parts for water, or the water is Roblox Terrain, leave the Water folder empty

![image](https://github.com/user-attachments/assets/6e10f18f-bbe3-4aa6-80b6-72e7332aadf7)

### 5.3 MaxHeight/MinHeight
- Place the MaxHeight/MinHeight parts at the maximum/minimum heights towers can be placed respectively
- For example, the MaxHeight/MinHeight on this map might be this rock formation/slightly below the start of the cliff respectively

![image](https://github.com/user-attachments/assets/00b1e5ff-c839-449b-b6e2-28cfcccbac3f)
_MaxHeight_

![image](https://github.com/user-attachments/assets/419080ce-0ae0-4ca4-b7c6-1a93d7e334fd)
_MinHeight_

### 5.4 RangeDisplayHeight
- On most maps, this is not needed. You can just leave this part as it is

## 6. SpawnLocation
- Place this somewhere near the middle of the map, perhaps favoring towards where the entrance is
- Feel free to adjust the appearance/transparency of the spawn

![image](https://github.com/user-attachments/assets/fdf8a7fd-81d7-4b1c-9dc7-f63d18fedc22)

## 7. PathHighlight
- Place all parts that should be highlighted during placement in here

![image](https://github.com/user-attachments/assets/79066f90-bc21-4415-94e8-6c08e73f9073)

## 8. Map
- All other parts in your map should be placed inside this model
- These objects will block LOS and will be included in raycasts

![image](https://github.com/user-attachments/assets/87db141a-974b-4587-b3c7-be32adb8de64)

## 9. LightingData
- We need to save the settings you have set in Lighting. In Studio, select the LightingData object. Make sure this is the only thing you have selected

![image](https://github.com/user-attachments/assets/4bcf7e76-486a-4fa5-867b-bebeae2e6258)

- Then, copy the following code and run it in the command bar
```lua
-- Write lighting data to config
local Lighting = game:GetService("Lighting")
local Config = game.Selection:Get()[1]

for Attribute, Value in Config:GetAttributes() do
	local LightingValue = Lighting[Attribute]

	if LightingValue then
		Config:SetAttribute(Attribute, LightingValue)
		print(tostring(Attribute) .. ": " .. tostring(Value) .. " -> " .. tostring(LightingValue))

		if Attribute == "ClockTime" and LightingValue < 0 then
			warn("ClockTime is negative!!!")
		end
	else
		warn(tostring(Attribute) .. " not found in Lighting")
	end
end
```

- You should see that your Lighting settings such as Ambient should be copied over to this object

![image](https://github.com/user-attachments/assets/1db57549-f188-4505-9bfd-f91c055459da)

## 10. Nodes
- Last step will be to place the nodes

![image](https://github.com/user-attachments/assets/fdc6b919-58af-44be-ae56-bc2603802217)

- Place the Spawn1 and End nodes in the entrance/exit respectively. The nodes should be halfway inside the entrance/exit

![image](https://github.com/user-attachments/assets/254d0661-4239-4d78-85d1-6482566b06d8)

![image](https://github.com/user-attachments/assets/e36a25f5-4697-46c3-8d5d-9c059f0d4f34)

- The **center** of each node part is used as the location for that node. Hence make sure the center is on the surface of whatever the enemies should be walking on

![image](https://github.com/user-attachments/assets/e2f80dff-65d1-4bd5-86b0-996717c1809c)

- For slopes, ensure any point where there is a change in the slope contains a node. The node should be centered around wherever the change in slope occurs

![image](https://github.com/user-attachments/assets/1d10b57a-b3f6-4b97-b055-a65522309863)

![image](https://github.com/user-attachments/assets/8c86d254-21c9-4bb6-952b-32c9ee52d913)

- Once all nodes are placed, we need to join the nodes. Select the nodes sequentially, starting from Spawn1, then selecting all the nodes in order, then finally selecting End. Once all nodes are selected in the proper order, run the following code in the command bar
```lua
local Selections = game.Selection:Get()

for i = 1, #Selections - 1 do
	local Node1 = Selections[i]
	local Node2 = Selections[i + 1]
	Node1.Next.Value = Node2
end
```

- You do not need a lot of nodes as my code smoothes out the movement automatically. This is how the nodes look in Singularity for example

![image](https://github.com/user-attachments/assets/85216fbc-8c80-4ac5-8d5e-6e786ce8962a)

