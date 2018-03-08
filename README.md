-----------------------------------------------------------------------------------------
-- 
-- main.lua
-- 
-- Created by: Aayman Shameem
-- Created on Mar 3 2018
-- 
-- This code makes an object scroll across the screen
-----------------------------------------------------------------------------------------

-- hide the status bar
display.setStatusBar(display.HiddenStatusBar)

-- local variables to this entire file
local scrollSpeed = 3

-- background image with width and height
local backgroundImage = display.newImageRect("./assets/textures/graveyard.png", 512, 384)
backgroundImage.x = display.contentCenterX
backgroundImage.y = display.contentCenterY
backgroundImage.id = "graveyard image background"

-- ghost image with width and height
local ghost = display.newImageRect("./assets/sprites/ghost.png", 70, 101)
ghost: setFillColor( 1, 1, 1 )
ghost.x = 0
ghost.y = display.contentHeight - 100 -- not using the center but the height of the display
ghost.id = "ghost"
ghost.alpha = 1.0 -- opaque at start

local bat = display.newImageRect("./assets/sprites/bat.png", 50.5, 35)
bat.x = display.contentWidth
bat.y = display.contentHeight - 100 -- not using the center but the height of the display
bat.id = "bat"
bat.alpha = 0 -- transparent at start

local function MoveImage( event )

	-- Object 1 --> ghost
	-- ghost movement right 
	-- add the scroll speed to the x-value of the image
	ghost.x = ghost.x + scrollSpeed
	-- changing ghost opacity to fade out
	ghost.alpha = ghost.alpha - 0.005
	-- decreases size
	ghost.height = ghost.height - 0.5
	ghost.width = ghost.width - 0.5
	ghost.rotation = ghost.rotation + 25
	
	

	-- Object 2 --> bat
	-- bat movement left
	bat.x = bat.x - scrollSpeed + 1
	bat.y = -0.0025*(bat.x - 180)*(bat.x - 180) + 80
	-- changing bat opacity to fade in
	bat.alpha = bat.alpha + 0.005

	



	print( display.fps ) -- this display how fast the current refresh is
end

-- MoveShip will be called at program start over and over (60 frames or times per second)
Runtime:addEventListener("enterFrame", MoveImage)
