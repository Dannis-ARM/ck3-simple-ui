# 🔍 CK3 1.21 ("Florin") 무역 & 도시/구역 바닐라 GUI 1차 조사

**바닐라 경로**: `C:\Program Files (x86)\Steam\steamapps\common\Crusader Kings III\game\gui\`

---

## 1. 핵심 바닐라 GUI 파일 맵

| 영역 | 파일명 | 줄 수 | 주요 `type` / 역할 |
| :--- | :--- | ---: | :--- |
| **영지/도시/구역** | `window_county_view.gui` | 8,665 | `holding_stats_sidebar`, `county_holding_stat`, `widget_top_county_info` (영지·구역 건설, 식량·번영도 메인 창) |
| **지역 시장** | `window_trade_market.gui` | 4,286 | `hbox_trade_market_header`, `market_balance_mode_toggle`, `market_good_balance_cell` (시장 수급표, 교역품 밸런스) |
| **무역 메인** | `window_trade.gui` | 3,684 | `widget_profit_trade_route_item`, `widget_distribution_trade_route_item`, `widget_commission_trade_route_item` (수익/배분/위탁 교역로 목록) |
| **교역로 플래너** | `window_trade_route_planner.gui` | 2,702 | `window_trade_route_planner_needs`, `vbox_route_needs_summary`, `confirm_body_needs`, `confirm_body_profit` |
| **수요/필요 위젯** | `shared\trade_needs.gui` | 1,027 | `vbox_market_needs`, `vbox_market_holding_needs`, `trade_needs_holdings_list` (영지별 식량·품목 수요 공용 위젯) |
| **교역품 상세** | `window_trade_good.gui` | 235 | `vbox_same_category_goods`, `active_trade_good_vbox` |
| **시장 점유율** | `shared\trade_market_share.gui` | 109 | `flowcontainer_trade_market_share_pie` |

---

## 2. Simple UI 설계 전략 (초안)

바닐라 핵심 창(`window_county_view.gui` 8.6k줄, `window_trade_market.gui` 4.2k줄)은 매우 방대하므로, **통파일 오버라이드를 피하고** 다음 2트랙으로 접근하는 것이 안전합니다.

1. **트랙 A (완전 비침습 — 독립 요약 패널 `sui_overview_window.gui`)**:
   * 바닐라 파일을 전혀 덮어쓰지 않고, HUD에 작은 버튼 하나만 추가해 **내 영지(식량/구역/시너지) + 내 시장(부족/잉여)**을 한눈에 보는 심플 대시보드를 띄움.
2. **트랙 B (최소 침습 — 핵심 위젯 요약 강화)**:
   * `shared\trade_needs.gui`나 `window_county_view.gui`의 상단 요약 영역에 `# [SUI] START ~ END` 마커로 **신호등(여유/부족/위험) 배지**만 깔끔하게 삽입.
