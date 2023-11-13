//@version=5
indicator("BREAKER BLOCK SAN", shorttitle="BREAKER BLOCK SAN", overlay=true, max_boxes_count=20)
showBreakerZoneSup = input.bool(title="Show Breaker Zone Support Areas", defval=true)
showBreakerZoneRes = input.bool(title="Show Breaker Zone Resistance Areas", defval=true)
boxSize = input.int(20, minval=1, title="Breaker Zone Width")
boxType = input.string(title="Breaker Zone Heigh", defval="OC", options=["OC", "HL"])

breakerZoneForLong =  (close > open) and (close[1] > open[1]) and (close > close[1]) and (close[2] < open[2]) and (close[2] > close[4]) and (close[3] > open[3]) and (close[4] > open[4]) and (close[3] > close[4])
if breakerZoneForLong and showBreakerZoneSup
    box.new(bar_index[2], boxType == "OC" ? close[2] : high[2], bar_index + boxSize, boxType == "OC" ? open[2] : low[2], bgcolor=color.new(color.blue, 70), border_color=color.blue)

breakerZoneForShort =  (close < open) and (close[1] < open[1]) and (close < close[1]) and (close[2] > open[2]) and (close[2] < close[4]) and (close[3] < open[3]) and (close[4] < open[4] and (close[3] < close[4]))
if breakerZoneForShort and showBreakerZoneRes
    box.new(bar_index[2], boxType == "OC" ? close[2] : high[2], bar_index + boxSize, boxType == "OC" ? open[2] : low[2], bgcolor=color.new(color.red, 70), border_color=color.red)
