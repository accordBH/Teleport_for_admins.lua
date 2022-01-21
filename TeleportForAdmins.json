require "lib.moonloader"
local wm = require 'windows.message'
local keys = require "vkeys"
local imgui = require "imgui"
local encoding = require 'encoding'
local sampev = require 'samp.events'
encoding.default = 'CP1251'
u8 = encoding.UTF8
local font = renderCreateFont("Arial", 10, 14)
local main_window_state = imgui.ImBool(false)
local text_buffer = imgui.ImBuffer(256)
local sw, sh = getScreenResolution()

script_version('2')

function update()
    local raw = 'https://raw.githubusercontent.com/GovnocodedByChapo/autoupdtest/main/file.json'
    local dlstatus = require('moonloader').download_status
    local requests = require('requests')
    local f = {}
    function f:getLastVersion()
        local response = requests.get(raw)
        if response.status_code == 200 then
            return decodeJson(response.text)['last']
        else
            return 'UNKNOWN'
        end
    end
    function f:download()
        local response = requests.get(raw)
        if response.status_code == 200 then
            downloadUrlToFile(decodeJson(response.text)['url'], thisScript().path, function (id, status, p1, p2)
                print('Скачиваю '..decodeJson(response.text)['url']..' в '..thisScript().path)
                if status == dlstatus.STATUSEX_ENDDOWNLOAD then
                    sampAddChatMessage('Скрипт обновлен, перезагрузка...', -1)
                    thisScript():reload()
                end
            end)
        else
            sampAddChatMessage('Ошибка, невозможно установить обновление, код: '..response.status_code, -1)
        end
    end
    return f
end

local coords = {
    {-2132, -748, 32,     'Автобазар'},
    {1131, -1412, 13,     'Центральный рынок'},
    {1506, -1291, 14,     'Правительство'},
    {1480, -1767, 18,	'Центральный банк'},
    {-502, 2595, 53,     'Автосалон LUXE'},
    {-2662, -62, 4,      'Автосалон PREMIUM'},
    {947, 2184, 10,     'Автосалон MEDIUM'},
    {-486, -555, 25,    'Автосалон LOW'},
    {2183, -1766, 13,     'The Rifa'},
    {2465, -1663, 13,     'Grove Street'},
    {2798, -1597, 10,     'Los-Santos Vagos'},
    {2016, -1135, 24,     'East Side Ballas'},
    {2503, -2007, 13,     'Varios Los Aztecas'},
    {2503, -1413, 28,     'Night Wolves'},
    {1515, 2773, 10,     'La Cosa Nostra'},
    {-2428, 138, 35,     'Yakuza'},
    {970, 1743, 8,         'Russian Mafia'},
    {-2192, -2355,  30,     'Warlock MC'},
	{1178, -1321, 14,		'Больница ЛС'},
	{-2663, 624, 14,	'Больница СФ'},
	{1619, 1827.4427490234, 10.8203125,		'Больница ЛВ'},
	{-2047.0498046875,   -76.459045410156,   35.165355682373,		'АвтоШкола'},
	{634.58612060547,   -574.13824462891,   16.3359375,		'RCPD'},
	{2287.3212890625,   2421.3989257813,   10.8203125,		'LVPD'},
	{1540.3236083984,   -1675.32421875,   13.540122032166,		'LSPD'},
	{ -1606.1019287109,   720.6044921875,   12.068364143372, 'SFPD'},
	{2637.4992675781,   1179.5935058594,   10.8203125,		'RLV'},
	{-1941.0119628906,   463.509765625,   35.171875,		'RSF'},
	{1653.9582519531,   -1662.7052001953,   22.515625,		'RLS'},
	{-1329.8363037109,   467.83905029297,   7.1875,	 'Авианосец'},
	{2733.7580566406,   -2397.3525390625,   13.6328125, 'Армия ЛС'},
	{170.4423828125,   1918.4233398438,   18.285482406616, 'Зона 51'},
	{ -2433.4770507813,   504.95321655273,   29.930027008057, 'FBI'}
}

function main()
    while not isSampAvailable() do wait(200) end
	
	sampAddChatMessage('{FFA500}[TP for Admins]: {ffffff}Успешно загружен. Автор: {80bcff}See_Rose', color)

    _, id = sampGetPlayerIdByCharHandle(PLAYER_PED)
    nick = sampGetPlayerNickname(id)

    sampRegisterChatCommand('tpp', cmd_imgui)

    imgui.Process = false

    addEventHandler('onWindowMessage', function(msg, wparam, lparam)
        if msg == wm.WM_KEYDOWN or msg == wm.WM_SYSKEYDOWN then
        end
    end)

    while true do
        wait(0)

        if main_window_state.v == false then
            imgui.Process = false
        end

    end
end

function cmd_imgui(arg)
    main_window_state.v = not main_window_state.v
    imgui.Process = main_window_state.v
end

function imgui.OnDrawFrame()

    imgui.SetNextWindowSize(imgui.ImVec2(600, 270), imgui.Cond.FirstUseEver)
    imgui.SetNextWindowPos(imgui.ImVec2(sw/2, sh/2), imgui.Cond.FirstUseEver, imgui.ImVec2(0.5, 0.5))	
		
    imgui.Begin("Teleport for Admins by See_Rose", main_window_state, imgui.WindowFlags.NoResize)
    --imgui.CenterText()
    imgui.Text(u8"Выберите место для телепорта")
    imgui.Separator()	

    imgui.Text(u8"Важные места:")
    if imgui.Button(u8"Автобазар") then
        setCharCoordinates(PLAYER_PED, coords[1][1], coords[1][2], coords[1][3])
    end
    imgui.SameLine()
    if imgui.Button(u8"Центральный рынок") then
        setCharCoordinates(PLAYER_PED, coords[2][1], coords[2][2], coords[2][3])
    end
    imgui.SameLine()
    if imgui.Button(u8"Правительство") then
        setCharCoordinates(PLAYER_PED, coords[3][1], coords[3][2], coords[3][3])
    end
    imgui.SameLine()
    if imgui.Button(u8"Центральный банк") then
        setCharCoordinates(PLAYER_PED, coords[4][1], coords[4][2], coords[4][3])
    end

    imgui.Text(u8"Автосалоны:")
    if imgui.Button(u8"LUXE") then
        setCharCoordinates(PLAYER_PED, coords[5][1], coords[5][2], coords[5][3])
    end
    imgui.SameLine()
    if imgui.Button(u8"PREMIUM") then
        setCharCoordinates(PLAYER_PED, coords[6][1], coords[6][2], coords[6][3])
    end
    imgui.SameLine()
    if imgui.Button(u8"MEDIUM") then
        setCharCoordinates(PLAYER_PED, coords[7][1], coords[7][2], coords[7][3])
    end
    imgui.SameLine()
    if imgui.Button(u8"LOW") then
        setCharCoordinates(PLAYER_PED, coords[8][1], coords[8][2], coords[8][3])
    end

    imgui.Text(u8"Банды:")
    if imgui.Button(u8"The Rifa") then
        setCharCoordinates(PLAYER_PED, coords[9][1], coords[9][2], coords[9][3])
    end
    imgui.SameLine()
    if imgui.Button(u8"Grove Street") then
        setCharCoordinates(PLAYER_PED, coords[10][1], coords[10][2], coords[10][3])
    end
    imgui.SameLine()
    if imgui.Button(u8"Los-Santos Vagos") then
        setCharCoordinates(PLAYER_PED, coords[11][1], coords[11][2], coords[11][3])
    end
    imgui.SameLine()
    if imgui.Button(u8"East Side Ballas") then
        setCharCoordinates(PLAYER_PED, coords[12][1], coords[12][2], coords[12][3])
    end
    imgui.SameLine()
    if imgui.Button(u8"Varios Los Aztecas") then
        setCharCoordinates(PLAYER_PED, coords[13][1], coords[13][2], coords[13][3])
    end
    imgui.SameLine()
    if imgui.Button(u8"Night Wolves") then
        setCharCoordinates(PLAYER_PED, coords[14][1], coords[14][2], coords[14][3])
    end

    imgui.Text(u8"Мафии:")
    if imgui.Button(u8"La Cosa Nostra") then
        setCharCoordinates(PLAYER_PED, coords[15][1], coords[15][2], coords[15][3])
    end
    imgui.SameLine()
    if imgui.Button(u8"Yakuza Mafia") then
        setCharCoordinates(PLAYER_PED, coords[16][1], coords[16][2], coords[16][3])
    end
    imgui.SameLine()
    if imgui.Button(u8"Russian Mafia") then
        setCharCoordinates(PLAYER_PED, coords[17][1], coords[17][2], coords[17][3])
    end
    imgui.SameLine()
    if imgui.Button(u8"Warlock MC") then
        setCharCoordinates(PLAYER_PED, coords[18][1], coords[18][2], coords[18][3])
    end
	imgui.Text(u8"Госс:")
    if imgui.Button(u8"Больница ЛС") then
        setCharCoordinates(PLAYER_PED, coords[19][1], coords[19][2], coords[19][3])
    end
	imgui.SameLine()
    if imgui.Button(u8"Больница СФ") then
        setCharCoordinates(PLAYER_PED, coords[20][1], coords[20][2], coords[20][3])
    end
	imgui.SameLine()
    if imgui.Button(u8"Больница ЛВ") then
        setCharCoordinates(PLAYER_PED, coords[21][1], coords[21][2], coords[21][3])
    end
	imgui.SameLine()
    if imgui.Button(u8"АвтоШкола") then
        setCharCoordinates(PLAYER_PED, coords[22][1], coords[22][2], coords[22][3])
    end
	imgui.SameLine()
    if imgui.Button(u8"RCPD") then
        setCharCoordinates(PLAYER_PED, coords[23][1], coords[23][2], coords[23][3])
    end
	imgui.SameLine()
    if imgui.Button(u8"LVPD") then
        setCharCoordinates(PLAYER_PED, coords[24][1], coords[24][2], coords[24][3])
    end
	imgui.SameLine()
    if imgui.Button(u8"LSPD") then
        setCharCoordinates(PLAYER_PED, coords[25][1], coords[25][2], coords[25][3])
    end
	imgui.SameLine()
    if imgui.Button(u8"SFPD") then
        setCharCoordinates(PLAYER_PED, coords[26][1], coords[26][2], coords[26][3])
    end
	imgui.NewLine()
    if imgui.Button(u8"RLV") then
        setCharCoordinates(PLAYER_PED, coords[27][1], coords[27][2], coords[27][3])
    end
	imgui.SameLine()
    if imgui.Button(u8"RSF") then
        setCharCoordinates(PLAYER_PED, coords[28][1], coords[28][2], coords[28][3])
    end
	imgui.SameLine()
    if imgui.Button(u8"RLS") then
        setCharCoordinates(PLAYER_PED, coords[29][1], coords[29][2], coords[29][3])
    end
	imgui.SameLine()
	if imgui.Button(u8"Авианосец") then
		setCharCoordinates(PLAYER_PED, coords[30][1], coords[30][2], coords[30][3])
	end
	imgui.SameLine()
	if imgui.Button(u8"Армия ЛС") then
		setCharCoordinates(PLAYER_PED, coords[31][1], coords[31][2], coords[31][3])
	end	
	imgui.SameLine()
	if imgui.Button(u8"Зона 51") then
		setCharCoordinates(PLAYER_PED, coords[32][1], coords[32][2], coords[32][3])
	end
	imgui.SameLine()
	if imgui.Button(u8"FBI") then
		setCharCoordinates(PLAYER_PED, coords[33][1], coords[33][2], coords[33][3])
	end	
	
    imgui.End()
end

function theme()
    imgui.SwitchContext()
    local style = imgui.GetStyle()
    local colors = style.Colors
    local clr = imgui.Col
    local ImVec4 = imgui.ImVec4
    local ImVec2 = imgui.ImVec2
    style.WindowPadding = ImVec2(6, 4)
    style.WindowRounding = 5.0
    style.ChildWindowRounding = 5.0
    style.FramePadding = ImVec2(5, 2)
    style.FrameRounding = 5.0
    style.ItemSpacing = ImVec2(7, 5)
    style.ItemInnerSpacing = ImVec2(1, 1)
    style.TouchExtraPadding = ImVec2(0, 0)
    style.IndentSpacing = 6.0
    style.ScrollbarSize = 12.0
    style.ScrollbarRounding = 5.0
    style.GrabMinSize = 20.0
    style.GrabRounding = 2.0
    style.WindowTitleAlign = ImVec2(0.5, 0.5)
    if ladno == false then
        colors[clr.Text]                   = ImVec4(1.00, 1.00, 1.00, 1.00)
        colors[clr.TextDisabled]           = ImVec4(0.28, 0.30, 0.35, 1.00)
        colors[clr.WindowBg]               = ImVec4(0.16, 0.18, 0.22, 1.00)
        colors[clr.ChildWindowBg]          = ImVec4(0.19, 0.22, 0.26, 1)
        colors[clr.PopupBg]                = ImVec4(0.05, 0.05, 0.10, 0.90)
        colors[clr.Border]                 = ImVec4(0.19, 0.22, 0.26, 1.00)
        colors[clr.BorderShadow]           = ImVec4(0.00, 0.00, 0.00, 0.00)
        colors[clr.FrameBg]                = ImVec4(0.16, 0.18, 0.22, 1.00)
        colors[clr.FrameBgHovered]         = ImVec4(0.22, 0.25, 0.30, 1.00)
        colors[clr.FrameBgActive]          = ImVec4(0.22, 0.25, 0.29, 1.00)
        colors[clr.TitleBg]                = ImVec4(0.19, 0.22, 0.26, 1.00)
        colors[clr.TitleBgActive]          = ImVec4(0.19, 0.22, 0.26, 1.00)
        colors[clr.TitleBgCollapsed]       = ImVec4(0.19, 0.22, 0.26, 0.59)
        colors[clr.MenuBarBg]              = ImVec4(0.19, 0.22, 0.26, 1.00)
        colors[clr.ScrollbarBg]            = ImVec4(0.20, 0.25, 0.30, 0.60)
        colors[clr.ScrollbarGrab]          = ImVec4(0.41, 0.55, 0.78, 1.00)
        colors[clr.ScrollbarGrabHovered]   = ImVec4(0.49, 0.63, 0.86, 1.00)
        colors[clr.ScrollbarGrabActive]    = ImVec4(0.49, 0.63, 0.86, 1.00)
        colors[clr.ComboBg]                = ImVec4(0.20, 0.20, 0.20, 0.99)
        colors[clr.CheckMark]              = ImVec4(0.90, 0.90, 0.90, 0.50)
        colors[clr.SliderGrab]             = ImVec4(1.00, 1.00, 1.00, 0.30)
        colors[clr.SliderGrabActive]       = ImVec4(0.80, 0.50, 0.50, 1.00)
        colors[clr.Button]                 = ImVec4(0.41, 0.55, 0.78, 1.00)
        colors[clr.ButtonHovered]          = ImVec4(0.49, 0.62, 0.85, 1.00)
        colors[clr.ButtonActive]           = ImVec4(0.49, 0.62, 0.85, 1.00)
        colors[clr.Header]                 = ImVec4(0.19, 0.22, 0.26, 1.00)
        colors[clr.HeaderHovered]          = ImVec4(0.22, 0.24, 0.28, 1.00)
        colors[clr.HeaderActive]           = ImVec4(0.22, 0.24, 0.28, 1.00)
        colors[clr.Separator]              = ImVec4(0.41, 0.55, 0.78, 1.00)
        colors[clr.SeparatorHovered]       = ImVec4(0.41, 0.55, 0.78, 1.00)
        colors[clr.SeparatorActive]        = ImVec4(0.41, 0.55, 0.78, 1.00)
        colors[clr.ResizeGrip]             = ImVec4(0.41, 0.55, 0.78, 1.00)
        colors[clr.ResizeGripHovered]      = ImVec4(0.49, 0.61, 0.83, 1.00)
        colors[clr.ResizeGripActive]       = ImVec4(0.49, 0.62, 0.83, 1.00)
        colors[clr.CloseButton]            = ImVec4(0.41, 0.55, 0.78, 1.00)
        colors[clr.CloseButtonHovered]     = ImVec4(0.50, 0.63, 0.84, 1.00)
        colors[clr.CloseButtonActive]      = ImVec4(0.41, 0.55, 0.78, 1.00)
        colors[clr.PlotLines]              = ImVec4(1.00, 1.00, 1.00, 1.00)
        colors[clr.PlotLinesHovered]       = ImVec4(0.90, 0.70, 0.00, 1.00)
        colors[clr.PlotHistogram]          = ImVec4(0.90, 0.70, 0.00, 1.00)
        colors[clr.PlotHistogramHovered]   = ImVec4(1.00, 0.60, 0.00, 1.00)
        colors[clr.TextSelectedBg]         = ImVec4(0.41, 0.55, 0.78, 1.00)
        colors[clr.ModalWindowDarkening]   = ImVec4(0.16, 0.18, 0.22, 0.76)
    else
        colors[clr.ChildWindowBg]          = ImVec4(0.19, 0.22, 0.26, 0)
        colors[clr.Border] = ImVec4(1, 0, 0.3, 1.00)
        colors[clr.WindowBg] = ImVec4(0.13, 0.14, 0.17, 1.00)
        colors[clr.FrameBg] = ImVec4(0.200, 0.220, 0.270, 0.85)
        colors[clr.TitleBg] = ImVec4(1, 0, 0.3, 1.00)
        colors[clr.TitleBgActive] = ImVec4(1, 0, 0.3, 1.00)
        colors[clr.Button] = ImVec4(1, 0, 0.3, 1.00)
        colors[clr.ButtonHovered] = ImVec4(1, 0, 0.3, 1.00)
        colors[clr.Separator] = ImVec4(1, 0, 0.3, 1.00)

        colors[clr.ResizeGrip]             = ImVec4(1, 0, 0.3, 1.00)
        colors[clr.ResizeGripHovered]      = ImVec4(1, 0, 0.3, 1.00)
        colors[clr.ResizeGripActive]       = ImVec4(1, 0, 0.3, 1.00)
       
        colors[clr.Header] = ImVec4(1, 0, 0.3, 1.00)
        colors[clr.HeaderHovered] = ImVec4(0.68, 0, 0.2, 0.86)
        colors[clr.HeaderActive] = ImVec4(1, 0.24, 0.47, 1.00)
        colors[clr.CheckMark] = ImVec4(1, 0, 0.3, 1.00)
        colors[clr.ModalWindowDarkening] = ImVec4(0.200, 0.220, 0.270, 0.73)

        colors[clr.ScrollbarBg] = ImVec4(0.200, 0.220, 0.270, 0.85)
        colors[clr.ScrollbarGrab] = ImVec4(1, 0, 0.3, 1.00)
        colors[clr.ScrollbarGrabHovered] = ImVec4(1, 0, 0.3, 1.00)
        colors[clr.ScrollbarGrabActive] = ImVec4(1, 0, 0.3, 1.00)

        colors[clr.ButtonActive] = ImVec4(1, 0, 0.3, 1.00)
    end
end
theme()
