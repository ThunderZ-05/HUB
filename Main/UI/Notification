-- Thanks to https://v3rmillion.net/showthread.php?tid=1212890
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")


local function Create(Name, Properties, Children)
    local Object = Instance.new(Name)
    for i, v in next, Properties or {} do
        Object[i] = v
    end
    for i, v in next, Children or {} do
		v.Parent = Object
	end
    return Object
end

local GUI = Create("ScreenGui", {
	Parent = game:GetService("CoreGui")
})

local NotificationHolder

function ThunderNotification(NotificationConfig)
	NotificationConfig.Title = NotificationConfig.Title or "Notification"
	NotificationConfig.Content = NotificationConfig.Content or "Content"
	NotificationConfig.Delay = NotificationConfig.Delay or 5

    if not NotificationHolder then
        NotificationHolder = Create("Frame", {
            Position = UDim2.new(1, -15, 1, -15),
            Size = UDim2.new(0, 230, 1, -15),
            AnchorPoint = Vector2.new(1, 1),
            BackgroundTransparency = 1,
            Parent = GUI,
            Name = "NotificationHolder"
        }, {
            Create("UIListLayout", {
                HorizontalAlignment = Enum.HorizontalAlignment.Center,
                SortOrder = Enum.SortOrder.LayoutOrder,
                VerticalAlignment = Enum.VerticalAlignment.Bottom
            })
        })
    end

    local NotificationBody = Create("TextButton", {
        Size = UDim2.new(1, 0, 0, 0),
		BackgroundTransparency = 1,
        Text = "",
		Parent = NotificationHolder,
        ZIndex = 1001,
    })

   -- local DurationBar = Create("Frame", {
       -- Parent = NotificationBody,
       -- Size = UDim2.new(1, -24, 0, 3),
       -- Position = UDim2.new(0, 12, 1, -12),
      --  BackgroundColor3 = Color3.fromRGB(37, 37, 37),
      --  BorderSizePixel = 0,
       -- ZIndex = 1002,
   -- }, {
    --    Create("UICorner", {CornerRadius = UDim.new(0, 3)})
    --})

    --local CloseButton = Create("TextButton", {
       -- Parent = NotificationBody,
       -- AnchorPoint = Vector2.new(1, 0.5),
      --  BackgroundColor3 = Color3.fromRGB(0, 0, 0),
       -- BackgroundTransparency = 0.900,
       -- BorderColor3 = Color3.fromRGB(0, 0, 0),
       -- BorderSizePixel = 0,
      --  Position = UDim2.new(1, 0, 0.81684494, -11),
       -- Size = UDim2.new(0, 24, 0, 24),
      --  Font = Enum.Font.SourceSans,
      --  Text = "",
     --   TextColor3 = Color3.fromRGB(0, 0, 0),
     --   TextSize = 14.000
 --   },  {
   --     Create("UICorner", { CornerRadius = UDim.new(0, 5) })
   -- })

    local NotificationFrame = Create("Frame", {
        Parent = NotificationBody,
        Size = UDim2.new(1, 0, 0, 0),
        Position = UDim2.new(1, 15, 0, 5),
        BackgroundColor3 = Color3.fromRGB(0, 27, 27),
        ZIndex = 1002,
    }, {
        Create("UICorner", {CornerRadius = UDim.new(0, 8)}),
        Create("TextLabel", {
            BackgroundTransparency = 1,
            Position = UDim2.new(0, 12, 0, 12),
            Size = UDim2.new(1, -24, 0, 10),
            Font = Enum.Font.GothamSemibold,
            Text = NotificationConfig.Title,
            TextXAlignment = Enum.TextXAlignment.Left,
            TextColor3 = Color3.fromRGB(0, 225, 225),
            TextSize = 13,
            RichText = true,
            Name = "Title",
            ZIndex = 1003,
        }),
        Create("TextLabel", {
            BackgroundTransparency = 1,
            Position = UDim2.new(0, 12, 0, 12),
            Size = UDim2.new(1, -48, 0, 10),
            Font = Enum.Font.GothamSemibold,
            Text = "",
            TextXAlignment = Enum.TextXAlignment.Right,
            TextColor3 = Color3.fromRGB(0, 225, 225),
            TextSize = 13,
            RichText = true,
            Name = "Time",
            ZIndex = 1003,
        }),
        Create("ImageButton", {
            Name = "Clear",
            AnchorPoint = Vector2.new(0.5, 0.5),
            BackgroundTransparency = 1.000,
            LayoutOrder = 3,
            Position = UDim2.new(0.5, 95, 0.5, -10),
            Size = UDim2.new(0, 18, 0, 18),
            ZIndex = 1003,
            Image = "rbxassetid://3926305904",
            ImageColor3 = Color3.fromRGB(200, 200, 200),
            ImageRectOffset = Vector2.new(924, 724),
            ImageRectSize = Vector2.new(36, 36)
        }),
        Create("TextLabel", {
            BackgroundTransparency = 1,
            Position = UDim2.new(0, 12, 0, 11),
            Size = UDim2.new(1, -24, 1, -15),
            Font = Enum.Font.Gotham,
            Text = NotificationConfig.Content,
            TextXAlignment = Enum.TextXAlignment.Left,
            TextColor3 = Color3.fromRGB(255, 255, 255),
            TextSize = 13,
            RichText = true,
            TextWrapped = true,
            Name = "Content",
            ZIndex = 1003,
        }),
        Create("Frame", {
            Parent = NotificationBody,
            Size = UDim2.new(1, -24, 0, 3),
            Position = UDim2.new(0, 12, 1, -12),
            BackgroundColor3 = Color3.fromRGB(0, 99, 99),
            BorderSizePixel = 0,
            ZIndex = 1003,
            Name = "DurationBar",
        }, {
            Create("UICorner", {CornerRadius = UDim.new(0, 3)})
        }),
        DurationBar,
        CloseButton
    })
    
    spawn(function()
		for i = NotificationConfig.Delay, 0, -1 do
			NotificationFrame.Time.Text = i .. "s"
			task.wait(1)
		end
	end)

    NotificationFrame.Clear.MouseEnter:Connect(function()
        TweenService:Create(NotificationFrame.Clear, TweenInfo.new(0.3, Enum.EasingStyle.Quint),
        { ImageColor3 = Color3.new(0.890196, 0.054902, 0.054902) }):Play()
    end)

    NotificationFrame.Clear.MouseLeave:Connect(function()
        TweenService:Create(NotificationFrame.Clear, TweenInfo.new(0.3, Enum.EasingStyle.Quint),
        { ImageColor3 = Color3.new(0.784314, 0.784314, 0.784314) }):Play()
    end)

    NotificationFrame.Size = UDim2.new(1, 0, 0, NotificationFrame.Content.TextBounds.Y + 42)
    TweenService:Create(NotificationBody,TweenInfo.new(0.25, Enum.EasingStyle.Quart, Enum.EasingDirection.Out),{Size = UDim2.new(1, 0, 0, NotificationFrame.Content.TextBounds.Y + 48)}):Play()
    TweenService:Create(NotificationFrame.DurationBar,TweenInfo.new(NotificationConfig.Delay, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),{Size = UDim2.new(0, 0, 0, 3)}):Play()
    TweenService:Create(NotificationFrame.DurationBar,TweenInfo.new(NotificationConfig.Delay, Enum.EasingStyle.Linear, Enum.EasingDirection.Out),{Size = UDim2.new(0, 0, 0, 3)}):Play()
    delay(0.15, function()
        TweenService:Create(NotificationFrame,TweenInfo.new(0.25, Enum.EasingStyle.Quart, Enum.EasingDirection.Out),{Position = UDim2.new(0,0,0,5)}):Play()
    end)

    NotificationFrame.Clear.MouseButton1Click:Connect(function()
        TweenService:Create(NotificationFrame,TweenInfo.new(0.25, Enum.EasingStyle.Quart, Enum.EasingDirection.Out),{Position = UDim2.new(1,15,0,5)}):Play()
        delay(0.15, function()
            TweenService:Create(NotificationBody,TweenInfo.new(0.25, Enum.EasingStyle.Quart, Enum.EasingDirection.Out),{Size = UDim2.new(1, 0, 0, 0)}):Play()
        end)
        delay(5,function() NotificationBody:Destroy() end)
    end)

    

    delay(NotificationConfig.Delay, function()
        TweenService:Create(NotificationFrame,TweenInfo.new(0.25, Enum.EasingStyle.Quart, Enum.EasingDirection.Out),{Position = UDim2.new(1,15,0,5)}):Play()
        delay(0.15, function()
            TweenService:Create(NotificationBody,TweenInfo.new(0.25, Enum.EasingStyle.Quart, Enum.EasingDirection.Out),{Size = UDim2.new(1, 0, 0, 0)}):Play()
        end)
        delay(5,function() NotificationBody:Destroy() end)
    end)
end

return ThunderNotification
