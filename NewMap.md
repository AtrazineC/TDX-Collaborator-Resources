# New map format
This guide will go over how to format a map properly for TDX.

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
- Name the template the name of the map ![image](https://github.com/user-attachments/assets/a57e0502-f216-44c0-b433-59633e4987ee)
- Put your name (preferably your Discord contact) in the Author `StringValue`. This is so I can contact you if there are issues ![image](https://github.com/user-attachments/assets/3bbf316e-2386-4f38-bab9-724b951c1cde)

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


## 2. LightingEffects
- Place all effects in Lighting such as `Sky`, `Bloom`, etc. instances in LightingEffects. 

![image](https://github.com/user-attachments/assets/44abaff3-7ae6-455d-8482-226068bbbe40)
