-- MonsterTransform.lua
-- سكربت يحول الشخصية إلى وحش عملاق

local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local rootPart = character:WaitForChild("HumanoidRootPart")

-- دالة التحول
local function transformToMonster()
    -- تكبير الشخصية 5 أضعاف
    for _, part in pairs(character:GetChildren()) do
        if part:IsA("BasePart") then
            part.Size = part.Size * 5
        elseif part:IsA("Accessory") and part:FindFirstChild("Handle") then
            part.Handle.Size = part.Handle.Size * 5
        end
    end

    -- زيادة الحركة والقفز
    humanoid.WalkSpeed = 40
    humanoid.JumpPower = 100

    -- تغيير اللون للون أحمر مخيف
    for _, part in pairs(character:GetChildren()) do
        if part:IsA("BasePart") then
            part.BrickColor = BrickColor.new("Really red")
        end
    end

    -- إضافة عيون مضيئة
    local head = character:FindFirstChild("Head")
    if head then
        local eye1 = Instance.new("PointLight", head)
        eye1.Color = Color3.new(1,0,0)
        eye1.Range = 15
        eye1.Brightness = 5
    end
end

-- التحول تلقائياً عند تشغيل السكربت
transformToMonster()
