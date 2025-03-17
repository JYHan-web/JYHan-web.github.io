import pandas as pd

# 경기 데이터를 기반으로 선수별 승패 기록을 계산하는 함수
def calculate_player_stats(tournaments):
    player_stats = {}
    
    for tournament in tournaments:
        for match in tournament["matches"]:
            player1, player2 = match["player1"], match["player2"]
            winner = match["winner"]
            
            if player1 not in player_stats:
                player_stats[player1] = {"승": 0, "패": 0}
            if player2 not in player_stats:
                player_stats[player2] = {"승": 0, "패": 0}
            
            if winner == player1:
                player_stats[player1]["승"] += 1
                player_stats[player2]["패"] += 1
            else:
                player_stats[player2]["승"] += 1
                player_stats[player1]["패"] += 1
    
    # 승률 계산 (승 / (승 + 패) * 100)
    for player in player_stats:
        total_matches = player_stats[player]["승"] + player_stats[player]["패"]
        if total_matches > 0:
            player_stats[player]["승률"] = round(player_stats[player]["승"] / total_matches * 100, 2)
        else:
            player_stats[player]["승률"] = 0.0
    
    return player_stats

{
  "tournaments": [
    {
      "name": "2022 1월 대한펜싱협회 유소년 국가대표선수 선발전",
      "location": "대한민국",
      "date": "2022-01",
      "division": "유소년",
      "weapon": "Epee",
      "round": "Preliminary",
      "teams": [
        {
          "team_name": "상안중학교",
          "members": [{"name": "김휘성", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "하길중학교",
          "members": [{"name": "고동연", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "인천해원중학교",
          "members": [{"name": "조희윤", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "동탄펜싱클럽",
          "members": [{"name": "김태형", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "대전탄방중학교",
          "members": [{"name": "엄선한", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "서울체육중학교",
          "members": [{"name": "이민서", "weapon": "Epee", "division": "유소년"}]
        }
      ],
      "matches": [
        {"player1": "김휘성", "player2": "고동연", "score": "1-5", "winner": "고동연"},
        {"player1": "김휘성", "player2": "조희윤", "score": "4-5", "winner": "조희윤"},
        {"player1": "김휘성", "player2": "김태형", "score": "2-5", "winner": "김태형"},
        {"player1": "김휘성", "player2": "엄선한", "score": "1-5", "winner": "엄선한"},
        {"player1": "김휘성", "player2": "이민서", "score": "2-5", "winner": "이민서"},
        {"player1": "고동연", "player2": "조희윤", "score": "5-3", "winner": "고동연"},
        {"player1": "고동연", "player2": "김태형", "score": "5-4", "winner": "고동연"},
        {"player1": "고동연", "player2": "엄선한", "score": "5-2", "winner": "고동연"},
        {"player1": "고동연", "player2": "이민서", "score": "5-3", "winner": "고동연"},
        {"player1": "조희윤", "player2": "김태형", "score": "3-5", "winner": "김태형"},
        {"player1": "조희윤", "player2": "엄선한", "score": "2-5", "winner": "조희윤"},
        {"player1": "조희윤", "player2": "이민서", "score": "0-5", "winner": "이민서"},
        {"player1": "김태형", "player2": "엄선한", "score": "4-5", "winner": "김태형"},
        {"player1": "김태형", "player2": "이민서", "score": "0-5", "winner": "이민서"},
        {"player1": "엄선한", "player2": "이민서", "score": "3-5", "winner": "이민서"}
      ]
    }
  ]
}
{
  "tournaments": [
    {
      "name": "2022 1월 대한펜싱협회 유소년 국가대표선수 선발전",
      "location": "대한민국",
      "date": "2022-01",
      "division": "유소년",
      "weapon": "Epee",
      "round": "Preliminary",
      "teams": [
        {
          "team_name": "중경고등학교",
          "members": [{"name": "김무현", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "진주제일중학교",
          "members": [{"name": "김민성", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "부산체육고등학교",
          "members": [{"name": "김성수", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "해남제일중학교",
          "members": [{"name": "이도협", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "서울체육중학교",
          "members": [{"name": "권윤찬", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "익산부천중학교",
          "members": [{"name": "한건희", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "대전탄방중학교",
          "members": [{"name": "정은수", "weapon": "Epee", "division": "유소년"}]
        }
      ],
      "matches": [
        {"player1": "김무현", "player2": "김민성", "score": "4-5", "winner": "김민성"},
        {"player1": "김무현", "player2": "김성수", "score": "4-5", "winner": "김성수"},
        {"player1": "김무현", "player2": "이도협", "score": "5-4", "winner": "김무현"},
        {"player1": "김무현", "player2": "권윤찬", "score": "5-2", "winner": "김무현"},
        {"player1": "김무현", "player2": "한건희", "score": "5-2", "winner": "김무현"},
        {"player1": "김무현", "player2": "정은수", "score": "5-1", "winner": "김무현"},
        {"player1": "김민성", "player2": "김성수", "score": "5-2", "winner": "김민성"},
        {"player1": "김민성", "player2": "이도협", "score": "5-3", "winner": "김민성"},
        {"player1": "김민성", "player2": "권윤찬", "score": "5-4", "winner": "김민성"},
        {"player1": "김민성", "player2": "한건희", "score": "5-3", "winner": "김민성"},
        {"player1": "김민성", "player2": "정은수", "score": "5-0", "winner": "김민성"},
        {"player1": "김성수", "player2": "이도협", "score": "3-5", "winner": "이도협"},
        {"player1": "김성수", "player2": "권윤찬", "score": "5-4", "winner": "김성수"},
        {"player1": "김성수", "player2": "한건희", "score": "5-3", "winner": "김성수"},
        {"player1": "김성수", "player2": "정은수", "score": "5-2", "winner": "김성수"},
        {"player1": "이도협", "player2": "권윤찬", "score": "4-5", "winner": "권윤찬"},
        {"player1": "이도협", "player2": "한건희", "score": "5-2", "winner": "이도협"},
        {"player1": "이도협", "player2": "정은수", "score": "5-4", "winner": "이도협"},
        {"player1": "권윤찬", "player2": "한건희", "score": "5-3", "winner": "권윤찬"},
        {"player1": "권윤찬", "player2": "정은수", "score": "5-3", "winner": "권윤찬"},
        {"player1": "한건희", "player2": "정은수", "score": "5-3", "winner": "한건희"}
      ]
    }
  ]
}
{
  "tournaments": [
    {
      "name": "2022 1월 대한펜싱협회 유소년 국가대표선수 선발전",
      "location": "대한민국",
      "date": "2022-01",
      "division": "유소년",
      "weapon": "Epee",
      "round": "Preliminary",
      "teams": [
        {
          "team_name": "경남체육고등학교",
          "members": [{"name": "김승범", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "서울체육중학교",
          "members": [{"name": "윤영도", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "전북체육고등학교",
          "members": [{"name": "박효렬", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "태화중학교",
          "members": [{"name": "이준현", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "진주제일중학교",
          "members": [{"name": "최정휴", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "대전펜싱클럽",
          "members": [{"name": "윙베르윌리암가브리엘", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "대전탄방중학교",
          "members": [{"name": "이민승", "weapon": "Epee", "division": "유소년"}]
        }
      ],
      "matches": [
        {"player1": "김승범", "player2": "윤영도", "score": "1-5", "winner": "윤영도"},
        {"player1": "김승범", "player2": "박효렬", "score": "5-3", "winner": "김승범"},
        {"player1": "김승범", "player2": "이준현", "score": "5-3", "winner": "김승범"},
        {"player1": "김승범", "player2": "최정휴", "score": "4-5", "winner": "최정휴"},
        {"player1": "김승범", "player2": "윙베르윌리암가브리엘", "score": "5-1", "winner": "김승범"},
        {"player1": "김승범", "player2": "이민승", "score": "5-1", "winner": "김승범"},
        
        {"player1": "윤영도", "player2": "김승범", "score": "5-1", "winner": "윤영도"},
        {"player1": "윤영도", "player2": "박효렬", "score": "1-5", "winner": "박효렬"},
        {"player1": "윤영도", "player2": "이준현", "score": "5-3", "winner": "윤영도"},
        {"player1": "윤영도", "player2": "최정휴", "score": "2-5", "winner": "최정휴"},
        {"player1": "윤영도", "player2": "윙베르윌리암가브리엘", "score": "5-1", "winner": "윤영도"},
        {"player1": "윤영도", "player2": "이민승", "score": "5-1", "winner": "윤영도"},
        
        {"player1": "박효렬", "player2": "김승범", "score": "3-5", "winner": "김승범"},
        {"player1": "박효렬", "player2": "윤영도", "score": "5-1", "winner": "박효렬"},
        {"player1": "박효렬", "player2": "이준현", "score": "1-5", "winner": "이준현"},
        {"player1": "박효렬", "player2": "최정휴", "score": "2-5", "winner": "최정휴"},
        {"player1": "박효렬", "player2": "윙베르윌리암가브리엘", "score": "2-5", "winner": "윙베르윌리암가브리엘"},
        {"player1": "박효렬", "player2": "이민승", "score": "2-5", "winner": "이민승"},
        
        {"player1": "이준현", "player2": "김승범", "score": "3-5", "winner": "김승범"},
        {"player1": "이준현", "player2": "윤영도", "score": "1-5", "winner": "윤영도"},
        {"player1": "이준현", "player2": "박효렬", "score": "5-1", "winner": "이준현"},
        {"player1": "이준현", "player2": "최정휴", "score": "5-2", "winner": "이준현"},
        {"player1": "이준현", "player2": "윙베르윌리암가브리엘", "score": "5-1", "winner": "이준현"},
        {"player1": "이준현", "player2": "이민승", "score": "5-1", "winner": "이준현"},
        
        {"player1": "최정휴", "player2": "김승범", "score": "5-4", "winner": "최정휴"},
        {"player1": "최정휴", "player2": "윤영도", "score": "5-2", "winner": "최정휴"},
        {"player1": "최정휴", "player2": "박효렬", "score": "5-2", "winner": "최정휴"},
        {"player1": "최정휴", "player2": "이준현", "score": "5-4", "winner": "최정휴"},
        {"player1": "최정휴", "player2": "윙베르윌리암가브리엘", "score": "5-1", "winner": "최정휴"},
        {"player1": "최정휴", "player2": "이민승", "score": "5-1", "winner": "최정휴"},
        
        {"player1": "윙베르윌리암가브리엘", "player2": "김승범", "score": "1-5", "winner": "김승범"},
        {"player1": "윙베르윌리암가브리엘", "player2": "윤영도", "score": "2-5", "winner": "윤영도"},
        {"player1": "윙베르윌리암가브리엘", "player2": "박효렬", "score": "5-2", "winner": "윙베르윌리암가브리엘"},
        {"player1": "윙베르윌리암가브리엘", "player2": "이준현", "score": "3-5", "winner": "이준현"},
        {"player1": "윙베르윌리암가브리엘", "player2": "최정휴", "score": "4-5", "winner": "최정휴"},
        {"player1": "윙베르윌리암가브리엘", "player2": "이민승", "score": "5-1", "winner": "윙베르윌리암가브리엘"}
      ]
    }
  ]
}
{
  "tournaments": [
    {
      "name": "2022 1월 대한펜싱협회 유소년 국가대표선수 선발전",
      "location": "대한민국",
      "date": "2022-01",
      "division": "유소년",
      "weapon": "Epee",
      "round": "Preliminary",
      "teams": [
        {
          "team_name": "중경고등학교",
          "members": [{"name": "김태민", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "해남공업고등학교",
          "members": [{"name": "오연수", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "동탄펜싱클럽",
          "members": [{"name": "최찬영", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "남산중학교",
          "members": [{"name": "김민재", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "대전문정중학교",
          "members": [{"name": "김동원", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "은호펜싱클럽",
          "members": [{"name": "한지윤", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "대전펜싱클럽",
          "members": [{"name": "정연우", "weapon": "Epee", "division": "유소년"}]
        }
      ],
      "matches": [
        {"player1": "김태민", "player2": "오연수", "score": "2-5", "winner": "오연수"},
        {"player1": "김태민", "player2": "최찬영", "score": "5-2", "winner": "김태민"},
        {"player1": "김태민", "player2": "김동원", "score": "5-3", "winner": "김태민"},
        {"player1": "김태민", "player2": "김민재", "score": "0-5", "winner": "김민재"},
        {"player1": "김태민", "player2": "한지윤", "score": "3-5", "winner": "한지윤"},
        {"player1": "김태민", "player2": "정연우", "score": "5-1", "winner": "김태민"},
        
        {"player1": "오연수", "player2": "김태민", "score": "3-5", "winner": "김태민"},
        {"player1": "오연수", "player2": "최찬영", "score": "5-2", "winner": "오연수"},
        {"player1": "오연수", "player2": "김동원", "score": "3-5", "winner": "김동원"},
        {"player1": "오연수", "player2": "김민재", "score": "1-5", "winner": "김민재"},
        {"player1": "오연수", "player2": "한지윤", "score": "2-5", "winner": "한지윤"},
        {"player1": "오연수", "player2": "정연우", "score": "5-1", "winner": "오연수"},
        
        {"player1": "최찬영", "player2": "김태민", "score": "2-5", "winner": "김태민"},
        {"player1": "최찬영", "player2": "오연수", "score": "3-5", "winner": "오연수"},
        {"player1": "최찬영", "player2": "김동원", "score": "2-5", "winner": "김동원"},
        {"player1": "최찬영", "player2": "김민재", "score": "1-5", "winner": "김민재"},
        {"player1": "최찬영", "player2": "한지윤", "score": "3-5", "winner": "한지윤"},
        {"player1": "최찬영", "player2": "정연우", "score": "5-2", "winner": "최찬영"},
        
        {"player1": "김동원", "player2": "김태민", "score": "2-5", "winner": "김태민"},
        {"player1": "김동원", "player2": "오연수", "score": "5-3", "winner": "김동원"},
        {"player1": "김동원", "player2": "최찬영", "score": "5-3", "winner": "김동원"},
        {"player1": "김동원", "player2": "김민재", "score": "1-5", "winner": "김민재"},
        {"player1": "김동원", "player2": "한지윤", "score": "3-5", "winner": "한지윤"},
        {"player1": "김동원", "player2": "정연우", "score": "5-2", "winner": "김동원"},
        
        {"player1": "김민재", "player2": "김태민", "score": "5-0", "winner": "김민재"},
        {"player1": "김민재", "player2": "오연수", "score": "5-1", "winner": "김민재"},
        {"player1": "김민재", "player2": "최찬영", "score": "5-1", "winner": "김민재"},
        {"player1": "김민재", "player2": "김동원", "score": "5-3", "winner": "김민재"},
        {"player1": "김민재", "player2": "한지윤", "score": "3-5", "winner": "한지윤"},
        {"player1": "김민재", "player2": "정연우", "score": "5-1", "winner": "김민재"},
        
        {"player1": "한지윤", "player2": "김태민", "score": "5-3", "winner": "한지윤"},
        {"player1": "한지윤", "player2": "오연수", "score": "5-2", "winner": "한지윤"},
        {"player1": "한지윤", "player2": "최찬영", "score": "5-3", "winner": "한지윤"},
        {"player1": "한지윤", "player2": "김동원", "score": "5-3", "winner": "한지윤"},
        {"player1": "한지윤", "player2": "김민재", "score": "5-3", "winner": "한지윤"},
        {"player1": "한지윤", "player2": "정연우", "score": "5-0", "winner": "한지윤"},
        
        {"player1": "정연우", "player2": "김태민", "score": "1-5", "winner": "김태민"},
        {"player1": "정연우", "player2": "오연수", "score": "1-5", "winner": "오연수"},
        {"player1": "정연우", "player2": "최찬영", "score": "2-5", "winner": "최찬영"},
        {"player1": "정연우", "player2": "김동원", "score": "5-3", "winner": "정연우"},
        {"player1": "정연우", "player2": "김민재", "score": "3-5", "winner": "김민재"},
        {"player1": "정연우", "player2": "한지윤", "score": "0-5", "winner": "한지윤"}
      ]
    }
  ]
}
{
  "tournaments": [
    {
      "name": "2022 1월 대한펜싱협회 유소년 국가대표선수 선발전",
      "location": "대한민국",
      "date": "2022-01",
      "division": "유소년",
      "weapon": "Epee",
      "round": "Preliminary",
      "teams": [
        {
          "team_name": "대전탄방중학교",
          "members": [{"name": "김희찬", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "전북체육고등학교",
          "members": [{"name": "김새힘", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "부산체육고등학교",
          "members": [{"name": "안무진", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "진주제일중학교",
          "members": [{"name": "이규한", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "태화중학교",
          "members": [{"name": "이상성", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "덕원중학교",
          "members": [{"name": "김성보", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "대전문정중학교",
          "members": [{"name": "이준우", "weapon": "Epee", "division": "유소년"}]
        }
      ],
      "matches": [
        {"player1": "김희찬", "player2": "김새힘", "score": "4-5", "winner": "김새힘"},
        {"player1": "김희찬", "player2": "안무진", "score": "5-3", "winner": "김희찬"},
        {"player1": "김희찬", "player2": "이규한", "score": "5-2", "winner": "김희찬"},
        {"player1": "김희찬", "player2": "이상성", "score": "5-2", "winner": "김희찬"},
        {"player1": "김희찬", "player2": "김성보", "score": "5-1", "winner": "김희찬"},
        {"player1": "김희찬", "player2": "이준우", "score": "5-1", "winner": "김희찬"},
        
        {"player1": "김새힘", "player2": "김희찬", "score": "5-4", "winner": "김새힘"},
        {"player1": "김새힘", "player2": "안무진", "score": "5-3", "winner": "김새힘"},
        {"player1": "김새힘", "player2": "이규한", "score": "3-5", "winner": "이규한"},
        {"player1": "김새힘", "player2": "이상성", "score": "5-2", "winner": "김새힘"},
        {"player1": "김새힘", "player2": "김성보", "score": "5-1", "winner": "김새힘"},
        {"player1": "김새힘", "player2": "이준우", "score": "5-1", "winner": "김새힘"},
        
        {"player1": "안무진", "player2": "김희찬", "score": "3-5", "winner": "김희찬"},
        {"player1": "안무진", "player2": "김새힘", "score": "1-5", "winner": "김새힘"},
        {"player1": "안무진", "player2": "이규한", "score": "4-5", "winner": "이규한"},
        {"player1": "안무진", "player2": "이상성", "score": "5-2", "winner": "안무진"},
        {"player1": "안무진", "player2": "김성보", "score": "5-1", "winner": "안무진"},
        {"player1": "안무진", "player2": "이준우", "score": "5-1", "winner": "안무진"},
        
        {"player1": "이규한", "player2": "김희찬", "score": "2-5", "winner": "김희찬"},
        {"player1": "이규한", "player2": "김새힘", "score": "5-3", "winner": "이규한"},
        {"player1": "이규한", "player2": "안무진", "score": "5-4", "winner": "이규한"},
        {"player1": "이규한", "player2": "이상성", "score": "5-2", "winner": "이규한"},
        {"player1": "이규한", "player2": "김성보", "score": "5-1", "winner": "이규한"},
        {"player1": "이규한", "player2": "이준우", "score": "5-1", "winner": "이규한"},
        
        {"player1": "이상성", "player2": "김희찬", "score": "4-5", "winner": "김희찬"},
        {"player1": "이상성", "player2": "김새힘", "score": "2-5", "winner": "김새힘"},
        {"player1": "이상성", "player2": "안무진", "score": "4-5", "winner": "안무진"},
        {"player1": "이상성", "player2": "이규한", "score": "2-5", "winner": "이규한"},
        {"player1": "이상성", "player2": "김성보", "score": "5-4", "winner": "이상성"},
        {"player1": "이상성", "player2": "이준우", "score": "5-1", "winner": "이상성"},
        
        {"player1": "김성보", "player2": "김희찬", "score": "1-5", "winner": "김희찬"},
        {"player1": "김성보", "player2": "김새힘", "score": "3-5", "winner": "김새힘"},
        {"player1": "김성보", "player2": "안무진", "score": "3-5", "winner": "안무진"},
        {"player1": "김성보", "player2": "이규한", "score": "3-5", "winner": "이규한"},
        {"player1": "김성보", "player2": "이상성", "score": "2-5", "winner": "이상성"},
        {"player1": "김성보", "player2": "이준우", "score": "5-4", "winner": "김성보"},
        
        {"player1": "이준우", "player2": "김희찬", "score": "1-5", "winner": "김희찬"},
        {"player1": "이준우", "player2": "김새힘", "score": "1-5", "winner": "김새힘"},
        {"player1": "이준우", "player2": "안무진", "score": "2-5", "winner": "안무진"},
        {"player1": "이준우", "player2": "이규한", "score": "5-2", "winner": "이준우"},
        {"player1": "이준우", "player2": "이상성", "score": "3-5", "winner": "이상성"},
        {"player1": "이준우", "player2": "김성보", "score": "0-5", "winner": "김성보"}
      ]
    }
  ]
}
{
  "tournaments": [
    {
      "name": "2022 1월 대한펜싱협회 유소년 국가대표선수 선발전",
      "location": "대한민국",
      "date": "2022-01",
      "division": "유소년",
      "weapon": "Epee",
      "round": "Preliminary",
      "teams": [
        {
          "team_name": "인천해원중학교",
          "members": [{"name": "김찬현", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "진주제일중학교",
          "members": [{"name": "전유섭", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "부산체육고등학교",
          "members": [{"name": "이지성", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "태화중학교",
          "members": [{"name": "김재원(태화중)", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "상안중학교",
          "members": [{"name": "김재원(상안중)", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "서울체육중학교",
          "members": [{"name": "이동현", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "동탄펜싱클럽",
          "members": [{"name": "조이준", "weapon": "Epee", "division": "유소년"}]
        }
      ],
      "matches": [
        {"player1": "김찬현", "player2": "전유섭", "score": "5-4", "winner": "김찬현"},
        {"player1": "김찬현", "player2": "이지성", "score": "5-4", "winner": "김찬현"},
        {"player1": "김찬현", "player2": "김재원(태화중)", "score": "0-5", "winner": "김재원(태화중)"},
        {"player1": "김찬현", "player2": "김재원(상안중)", "score": "5-3", "winner": "김찬현"},
        {"player1": "김찬현", "player2": "이동현", "score": "5-2", "winner": "김찬현"},
        {"player1": "김찬현", "player2": "조이준", "score": "5-1", "winner": "김찬현"},

        {"player1": "전유섭", "player2": "김찬현", "score": "4-5", "winner": "김찬현"},
        {"player1": "전유섭", "player2": "이지성", "score": "5-3", "winner": "전유섭"},
        {"player1": "전유섭", "player2": "김재원(태화중)", "score": "3-5", "winner": "김재원(태화중)"},
        {"player1": "전유섭", "player2": "김재원(상안중)", "score": "5-2", "winner": "전유섭"},
        {"player1": "전유섭", "player2": "이동현", "score": "5-2", "winner": "전유섭"},
        {"player1": "전유섭", "player2": "조이준", "score": "5-1", "winner": "전유섭"},

        {"player1": "이지성", "player2": "김찬현", "score": "4-5", "winner": "김찬현"},
        {"player1": "이지성", "player2": "전유섭", "score": "4-5", "winner": "전유섭"},
        {"player1": "이지성", "player2": "김재원(태화중)", "score": "5-2", "winner": "이지성"},
        {"player1": "이지성", "player2": "김재원(상안중)", "score": "5-2", "winner": "이지성"},
        {"player1": "이지성", "player2": "이동현", "score": "5-2", "winner": "이지성"},
        {"player1": "이지성", "player2": "조이준", "score": "5-2", "winner": "이지성"},

        {"player1": "김재원(태화중)", "player2": "김찬현", "score": "5-1", "winner": "김재원(태화중)"},
        {"player1": "김재원(태화중)", "player2": "전유섭", "score": "5-2", "winner": "김재원(태화중)"},
        {"player1": "김재원(태화중)", "player2": "이지성", "score": "2-5", "winner": "이지성"},
        {"player1": "김재원(태화중)", "player2": "김재원(상안중)", "score": "2-5", "winner": "김재원(상안중)"},
        {"player1": "김재원(태화중)", "player2": "이동현", "score": "5-2", "winner": "김재원(태화중)"},
        {"player1": "김재원(태화중)", "player2": "조이준", "score": "5-2", "winner": "김재원(태화중)"},

        {"player1": "김재원(상안중)", "player2": "김찬현", "score": "2-5", "winner": "김찬현"},
        {"player1": "김재원(상안중)", "player2": "전유섭", "score": "2-5", "winner": "전유섭"},
        {"player1": "김재원(상안중)", "player2": "이지성", "score": "3-5", "winner": "이지성"},
        {"player1": "김재원(상안중)", "player2": "김재원(태화중)", "score": "5-2", "winner": "김재원(상안중)"},
        {"player1": "김재원(상안중)", "player2": "이동현", "score": "5-2", "winner": "김재원(상안중)"},
        {"player1": "김재원(상안중)", "player2": "조이준", "score": "5-2", "winner": "김재원(상안중)"},

        {"player1": "이동현", "player2": "김찬현", "score": "1-5", "winner": "김찬현"},
        {"player1": "이동현", "player2": "전유섭", "score": "2-5", "winner": "전유섭"},
        {"player1": "이동현", "player2": "이지성", "score": "2-5", "winner": "이지성"},
        {"player1": "이동현", "player2": "김재원(태화중)", "score": "2-5", "winner": "김재원(태화중)"},
        {"player1": "이동현", "player2": "김재원(상안중)", "score": "2-5", "winner": "김재원(상안중)"},
        {"player1": "이동현", "player2": "조이준", "score": "2-5", "winner": "조이준"}
      ]
    }
  ]
}
{
  "tournaments": [
    {
      "name": "2022 1월 대한펜싱협회 유소년 국가대표선수 선발전",
      "location": "대한민국",
      "date": "2022-01",
      "division": "유소년",
      "weapon": "Epee",
      "round": "Preliminary",
      "teams": [
        {
          "team_name": "광주체육고등학교",
          "members": [{"name": "주성연", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "진주제일중학교",
          "members": [{"name": "정수민", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "광주체육고등학교",
          "members": [{"name": "박지민", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "서울체육중학교",
          "members": [{"name": "이윤재", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "태화중학교",
          "members": [{"name": "조범진", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "덕원중학교",
          "members": [{"name": "김정식", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "동탄펜싱클럽",
          "members": [{"name": "이은파", "weapon": "Epee", "division": "유소년"}]
        }
      ],
      "matches": [
        {"player1": "주성연", "player2": "정수민", "score": "2-5", "winner": "정수민"},
        {"player1": "주성연", "player2": "박지민", "score": "5-3", "winner": "주성연"},
        {"player1": "주성연", "player2": "이윤재", "score": "5-3", "winner": "주성연"},
        {"player1": "주성연", "player2": "조범진", "score": "5-3", "winner": "주성연"},
        {"player1": "주성연", "player2": "김정식", "score": "4-5", "winner": "김정식"},
        {"player1": "주성연", "player2": "이은파", "score": "5-2", "winner": "주성연"},

        {"player1": "정수민", "player2": "주성연", "score": "5-2", "winner": "정수민"},
        {"player1": "정수민", "player2": "박지민", "score": "4-5", "winner": "박지민"},
        {"player1": "정수민", "player2": "이윤재", "score": "5-3", "winner": "정수민"},
        {"player1": "정수민", "player2": "조범진", "score": "5-3", "winner": "정수민"},
        {"player1": "정수민", "player2": "김정식", "score": "5-2", "winner": "정수민"},
        {"player1": "정수민", "player2": "이은파", "score": "5-0", "winner": "정수민"},

        {"player1": "박지민", "player2": "주성연", "score": "3-5", "winner": "주성연"},
        {"player1": "박지민", "player2": "정수민", "score": "5-4", "winner": "박지민"},
        {"player1": "박지민", "player2": "이윤재", "score": "5-3", "winner": "박지민"},
        {"player1": "박지민", "player2": "조범진", "score": "5-3", "winner": "박지민"},
        {"player1": "박지민", "player2": "김정식", "score": "5-2", "winner": "박지민"},
        {"player1": "박지민", "player2": "이은파", "score": "5-1", "winner": "박지민"},

        {"player1": "이윤재", "player2": "주성연", "score": "3-5", "winner": "주성연"},
        {"player1": "이윤재", "player2": "정수민", "score": "3-5", "winner": "정수민"},
        {"player1": "이윤재", "player2": "박지민", "score": "3-5", "winner": "박지민"},
        {"player1": "이윤재", "player2": "조범진", "score": "2-5", "winner": "조범진"},
        {"player1": "이윤재", "player2": "김정식", "score": "0-5", "winner": "김정식"},
        {"player1": "이윤재", "player2": "이은파", "score": "4-5", "winner": "이은파"},

        {"player1": "조범진", "player2": "주성연", "score": "3-5", "winner": "주성연"},
        {"player1": "조범진", "player2": "정수민", "score": "2-5", "winner": "정수민"},
        {"player1": "조범진", "player2": "박지민", "score": "4-5", "winner": "박지민"},
        {"player1": "조범진", "player2": "이윤재", "score": "5-2", "winner": "조범진"},
        {"player1": "조범진", "player2": "김정식", "score": "4-5", "winner": "김정식"},
        {"player1": "조범진", "player2": "이은파", "score": "5-2", "winner": "조범진"},

        {"player1": "김정식", "player2": "주성연", "score": "5-4", "winner": "김정식"},
        {"player1": "김정식", "player2": "정수민", "score": "2-5", "winner": "정수민"},
        {"player1": "김정식", "player2": "박지민", "score": "4-5", "winner": "박지민"},
        {"player1": "김정식", "player2": "이윤재", "score": "5-0", "winner": "김정식"},
        {"player1": "김정식", "player2": "조범진", "score": "5-4", "winner": "김정식"},
        {"player1": "김정식", "player2": "이은파", "score": "5-2", "winner": "김정식"},

        {"player1": "이은파", "player2": "주성연", "score": "2-5", "winner": "주성연"},
        {"player1": "이은파", "player2": "정수민", "score": "0-5", "winner": "정수민"},
        {"player1": "이은파", "player2": "박지민", "score": "1-5", "winner": "박지민"},
        {"player1": "이은파", "player2": "이윤재", "score": "5-4", "winner": "이은파"},
        {"player1": "이은파", "player2": "조범진", "score": "1-5", "winner": "조범진"},
        {"player1": "이은파", "player2": "김정식", "score": "3-5", "winner": "김정식"}
      ]
    }
  ]
}
{
  "tournaments": [
    {
      "name": "2022 1월 대한펜싱협회 유소년 국가대표선수 선발전",
      "location": "대한민국",
      "date": "2022-01",
      "division": "유소년",
      "weapon": "Epee",
      "round": "Preliminary",
      "teams": [
        {
          "team_name": "인천해원중학교",
          "members": [{"name": "김내훈", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "부산체육고등학교",
          "members": [{"name": "김현빈", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "광주체육고등학교",
          "members": [{"name": "서현준", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "두암중학교",
          "members": [{"name": "조용진", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "진주제일중학교",
          "members": [{"name": "오정민", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "하길중학교",
          "members": [{"name": "김민서", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "대전탄방중학교",
          "members": [{"name": "반승수", "weapon": "Epee", "division": "유소년"}]
        }
      ],
      "matches": [
        {"player1": "김내훈", "player2": "김현빈", "score": "3-5", "winner": "김현빈"},
        {"player1": "김내훈", "player2": "서현준", "score": "4-5", "winner": "서현준"},
        {"player1": "김내훈", "player2": "조용진", "score": "5-3", "winner": "김내훈"},
        {"player1": "김내훈", "player2": "오정민", "score": "5-2", "winner": "김내훈"},
        {"player1": "김내훈", "player2": "김민서", "score": "4-5", "winner": "김민서"},
        {"player1": "김내훈", "player2": "반승수", "score": "5-2", "winner": "김내훈"},

        {"player1": "김현빈", "player2": "김내훈", "score": "5-3", "winner": "김현빈"},
        {"player1": "김현빈", "player2": "서현준", "score": "5-4", "winner": "김현빈"},
        {"player1": "김현빈", "player2": "조용진", "score": "5-2", "winner": "김현빈"},
        {"player1": "김현빈", "player2": "오정민", "score": "5-2", "winner": "김현빈"},
        {"player1": "김현빈", "player2": "김민서", "score": "5-3", "winner": "김현빈"},
        {"player1": "김현빈", "player2": "반승수", "score": "5-1", "winner": "김현빈"},

        {"player1": "서현준", "player2": "김내훈", "score": "5-4", "winner": "서현준"},
        {"player1": "서현준", "player2": "김현빈", "score": "4-5", "winner": "김현빈"},
        {"player1": "서현준", "player2": "조용진", "score": "5-2", "winner": "서현준"},
        {"player1": "서현준", "player2": "오정민", "score": "5-2", "winner": "서현준"},
        {"player1": "서현준", "player2": "김민서", "score": "5-3", "winner": "서현준"},
        {"player1": "서현준", "player2": "반승수", "score": "5-1", "winner": "서현준"},

        {"player1": "조용진", "player2": "김내훈", "score": "3-5", "winner": "김내훈"},
        {"player1": "조용진", "player2": "김현빈", "score": "2-5", "winner": "김현빈"},
        {"player1": "조용진", "player2": "서현준", "score": "2-5", "winner": "서현준"},
        {"player1": "조용진", "player2": "오정민", "score": "4-5", "winner": "오정민"},
        {"player1": "조용진", "player2": "김민서", "score": "5-3", "winner": "조용진"},
        {"player1": "조용진", "player2": "반승수", "score": "5-1", "winner": "조용진"},

        {"player1": "오정민", "player2": "김내훈", "score": "2-5", "winner": "김내훈"},
        {"player1": "오정민", "player2": "김현빈", "score": "0-5", "winner": "김현빈"},
        {"player1": "오정민", "player2": "서현준", "score": "4-5", "winner": "서현준"},
        {"player1": "오정민", "player2": "조용진", "score": "5-4", "winner": "오정민"},
        {"player1": "오정민", "player2": "김민서", "score": "5-3", "winner": "오정민"},
        {"player1": "오정민", "player2": "반승수", "score": "5-2", "winner": "오정민"},

        {"player1": "김민서", "player2": "김내훈", "score": "5-4", "winner": "김민서"},
        {"player1": "김민서", "player2": "김현빈", "score": "2-5", "winner": "김현빈"},
        {"player1": "김민서", "player2": "서현준", "score": "4-5", "winner": "서현준"},
        {"player1": "김민서", "player2": "조용진", "score": "3-5", "winner": "조용진"},
        {"player1": "김민서", "player2": "오정민", "score": "3-5", "winner": "오정민"},
        {"player1": "김민서", "player2": "반승수", "score": "5-3", "winner": "김민서"},

        {"player1": "반승수", "player2": "김내훈", "score": "2-5", "winner": "김내훈"},
        {"player1": "반승수", "player2": "김현빈", "score": "1-5", "winner": "김현빈"},
        {"player1": "반승수", "player2": "서현준", "score": "4-5", "winner": "서현준"},
        {"player1": "반승수", "player2": "조용진", "score": "0-5", "winner": "조용진"},
        {"player1": "반승수", "player2": "오정민", "score": "4-5", "winner": "오정민"},
        {"player1": "반승수", "player2": "김민서", "score": "1-5", "winner": "김민서"}
      ]
    }
  ]
}
{
  "tournaments": [
    {
      "name": "2022 1월 대한펜싱협회 유소년 국가대표선수 선발전",
      "location": "대한민국",
      "date": "2022-01",
      "division": "유소년",
      "weapon": "Epee",
      "round": "Preliminary",
      "teams": [
        {
          "team_name": "인천해원중학교",
          "members": [{"name": "김내훈", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "부산체육고등학교",
          "members": [{"name": "김현빈", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "광주체육고등학교",
          "members": [{"name": "서현준", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "두암중학교",
          "members": [{"name": "조용진", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "진주제일중학교",
          "members": [{"name": "오정민", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "하길중학교",
          "members": [{"name": "김민서", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "대전탄방중학교",
          "members": [{"name": "반승수", "weapon": "Epee", "division": "유소년"}]
        }
      ],
      "matches": [
        {"player1": "김내훈", "player2": "김현빈", "score": "3-5", "winner": "김현빈"},
        {"player1": "김내훈", "player2": "서현준", "score": "4-5", "winner": "서현준"},
        {"player1": "김내훈", "player2": "조용진", "score": "5-3", "winner": "김내훈"},
        {"player1": "김내훈", "player2": "오정민", "score": "5-2", "winner": "김내훈"},
        {"player1": "김내훈", "player2": "김민서", "score": "4-5", "winner": "김민서"},
        {"player1": "김내훈", "player2": "반승수", "score": "5-2", "winner": "김내훈"},

        {"player1": "김현빈", "player2": "김내훈", "score": "5-3", "winner": "김현빈"},
        {"player1": "김현빈", "player2": "서현준", "score": "5-4", "winner": "김현빈"},
        {"player1": "김현빈", "player2": "조용진", "score": "5-2", "winner": "김현빈"},
        {"player1": "김현빈", "player2": "오정민", "score": "5-2", "winner": "김현빈"},
        {"player1": "김현빈", "player2": "김민서", "score": "5-3", "winner": "김현빈"},
        {"player1": "김현빈", "player2": "반승수", "score": "5-1", "winner": "김현빈"},

        {"player1": "서현준", "player2": "김내훈", "score": "5-4", "winner": "서현준"},
        {"player1": "서현준", "player2": "김현빈", "score": "4-5", "winner": "김현빈"},
        {"player1": "서현준", "player2": "조용진", "score": "5-2", "winner": "서현준"},
        {"player1": "서현준", "player2": "오정민", "score": "5-2", "winner": "서현준"},
        {"player1": "서현준", "player2": "김민서", "score": "5-3", "winner": "서현준"},
        {"player1": "서현준", "player2": "반승수", "score": "5-1", "winner": "서현준"},

        {"player1": "조용진", "player2": "김내훈", "score": "3-5", "winner": "김내훈"},
        {"player1": "조용진", "player2": "김현빈", "score": "2-5", "winner": "김현빈"},
        {"player1": "조용진", "player2": "서현준", "score": "2-5", "winner": "서현준"},
        {"player1": "조용진", "player2": "오정민", "score": "4-5", "winner": "오정민"},
        {"player1": "조용진", "player2": "김민서", "score": "5-3", "winner": "조용진"},
        {"player1": "조용진", "player2": "반승수", "score": "5-1", "winner": "조용진"},

        {"player1": "오정민", "player2": "김내훈", "score": "2-5", "winner": "김내훈"},
        {"player1": "오정민", "player2": "김현빈", "score": "0-5", "winner": "김현빈"},
        {"player1": "오정민", "player2": "서현준", "score": "4-5", "winner": "서현준"},
        {"player1": "오정민", "player2": "조용진", "score": "5-4", "winner": "오정민"},
        {"player1": "오정민", "player2": "김민서", "score": "5-3", "winner": "오정민"},
        {"player1": "오정민", "player2": "반승수", "score": "5-2", "winner": "오정민"},

        {"player1": "김민서", "player2": "김내훈", "score": "5-4", "winner": "김민서"},
        {"player1": "김민서", "player2": "김현빈", "score": "2-5", "winner": "김현빈"},
        {"player1": "김민서", "player2": "서현준", "score": "4-5", "winner": "서현준"},
        {"player1": "김민서", "player2": "조용진", "score": "3-5", "winner": "조용진"},
        {"player1": "김민서", "player2": "오정민", "score": "3-5", "winner": "오정민"},
        {"player1": "김민서", "player2": "반승수", "score": "5-3", "winner": "김민서"},

        {"player1": "반승수", "player2": "김내훈", "score": "2-5", "winner": "김내훈"},
        {"player1": "반승수", "player2": "김현빈", "score": "1-5", "winner": "김현빈"},
        {"player1": "반승수", "player2": "서현준", "score": "4-5", "winner": "서현준"},
        {"player1": "반승수", "player2": "조용진", "score": "0-5", "winner": "조용진"},
        {"player1": "반승수", "player2": "오정민", "score": "4-5", "winner": "오정민"},
        {"player1": "반승수", "player2": "김민서", "score": "1-5", "winner": "김민서"}
      ]
    }
  ]
}
{
  "tournaments": [
    {
      "name": "2022 1월 대한펜싱협회 유소년 국가대표선수 선발전",
      "location": "대한민국",
      "date": "2022-01",
      "division": "유소년",
      "weapon": "Epee",
      "round": "Preliminary",
      "teams": [
        {
          "team_name": "인천해원중학교",
          "members": [{"name": "김준수", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "불곡고등학교",
          "members": [{"name": "김민욱", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "광주체육중학교",
          "members": [{"name": "전수범", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "계룡중학교",
          "members": [{"name": "김태환", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "태화중학교",
          "members": [{"name": "김민준", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "남산중학교",
          "members": [{"name": "김성준", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "상안중학교",
          "members": [{"name": "안시언", "weapon": "Epee", "division": "유소년"}]
        }
      ],
      "matches": [
        {"player1": "김준수", "player2": "김민욱", "score": "2-5", "winner": "김민욱"},
        {"player1": "김준수", "player2": "전수범", "score": "2-5", "winner": "전수범"},
        {"player1": "김준수", "player2": "김태환", "score": "3-5", "winner": "김태환"},
        {"player1": "김준수", "player2": "김민준", "score": "3-5", "winner": "김민준"},
        {"player1": "김준수", "player2": "김성준", "score": "4-5", "winner": "김성준"},
        {"player1": "김준수", "player2": "안시언", "score": "5-2", "winner": "김준수"},
        {"player1": "김민욱", "player2": "김준수", "score": "5-2", "winner": "김민욱"},
        {"player1": "김민욱", "player2": "전수범", "score": "5-3", "winner": "김민욱"},
        {"player1": "김민욱", "player2": "김태환", "score": "5-4", "winner": "김민욱"},
        {"player1": "김민욱", "player2": "김민준", "score": "5-4", "winner": "김민욱"},
        {"player1": "김민욱", "player2": "김성준", "score": "5-2", "winner": "김민욱"},
        {"player1": "김민욱", "player2": "안시언", "score": "5-3", "winner": "김민욱"},
        {"player1": "전수범", "player2": "김준수", "score": "5-2", "winner": "전수범"},
        {"player1": "전수범", "player2": "김민욱", "score": "3-5", "winner": "김민욱"},
        {"player1": "전수범", "player2": "김태환", "score": "4-5", "winner": "김태환"},
        {"player1": "전수범", "player2": "김민준", "score": "5-3", "winner": "전수범"},
        {"player1": "전수범", "player2": "김성준", "score": "5-4", "winner": "전수범"},
        {"player1": "전수범", "player2": "안시언", "score": "5-2", "winner": "전수범"},
        {"player1": "김태환", "player2": "김준수", "score": "5-3", "winner": "김태환"},
        {"player1": "김태환", "player2": "김민욱", "score": "2-5", "winner": "김민욱"},
        {"player1": "김태환", "player2": "전수범", "score": "5-3", "winner": "김태환"},
        {"player1": "김태환", "player2": "김민준", "score": "5-4", "winner": "김태환"},
        {"player1": "김태환", "player2": "김성준", "score": "5-2", "winner": "김태환"},
        {"player1": "김태환", "player2": "안시언", "score": "5-3", "winner": "김태환"},
        {"player1": "김민준", "player2": "김준수", "score": "5-3", "winner": "김민준"},
        {"player1": "김민준", "player2": "김민욱", "score": "4-5", "winner": "김민욱"},
        {"player1": "김민준", "player2": "전수범", "score": "3-5", "winner": "전수범"},
        {"player1": "김민준", "player2": "김태환", "score": "2-5", "winner": "김태환"},
        {"player1": "김민준", "player2": "김성준", "score": "5-2", "winner": "김민준"},
        {"player1": "김민준", "player2": "안시언", "score": "5-3", "winner": "김민준"},
        {"player1": "김성준", "player2": "김준수", "score": "5-4", "winner": "김성준"},
        {"player1": "김성준", "player2": "김민욱", "score": "2-5", "winner": "김민욱"},
        {"player1": "김성준", "player2": "전수범", "score": "3-5", "winner": "전수범"},
        {"player1": "김성준", "player2": "김태환", "score": "4-5", "winner": "김태환"},
        {"player1": "김성준", "player2": "김민준", "score": "2-5", "winner": "김민준"},
        {"player1": "김성준", "player2": "안시언", "score": "5-3", "winner": "김성준"},
        {"player1": "안시언", "player2": "김준수", "score": "2-5", "winner": "김준수"},
        {"player1": "안시언", "player2": "김민욱", "score": "3-5", "winner": "김민욱"},
        {"player1": "안시언", "player2": "전수범", "score": "4-5", "winner": "전수범"},
        {"player1": "안시언", "player2": "김태환", "score": "5-3", "winner": "안시언"},
        {"player1": "안시언", "player2": "김민준", "score": "3-5", "winner": "김민준"},
        {"player1": "안시언", "player2": "김성준", "score": "3-5", "winner": "김성준"}
      ]
    }
  ]
}
{
  "tournaments": [
    {
      "name": "2022 1월 대한펜싱협회 유소년 국가대표선수 선발전",
      "location": "대한민국",
      "date": "2022-01",
      "division": "유소년",
      "weapon": "Epee",
      "round": "Preliminary",
      "teams": [
        {
          "team_name": "인천체육고등학교",
          "members": [{"name": "김인환", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "불곡고등학교",
          "members": [{"name": "조재찬", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "계룡중학교",
          "members": [{"name": "이륜호", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "서울체육중학교",
          "members": [{"name": "김서준", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "태화중학교",
          "members": [{"name": "송이헌", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "부산체육고등학교",
          "members": [{"name": "배준호", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "인천해원중학교",
          "members": [{"name": "김태오", "weapon": "Epee", "division": "유소년"}]
        }
      ],
      "matches": [
        {"player1": "김인환", "player2": "조재찬", "score": "4-5", "winner": "조재찬"},
        {"player1": "김인환", "player2": "이륜호", "score": "5-3", "winner": "김인환"},
        {"player1": "김인환", "player2": "김서준", "score": "2-5", "winner": "김서준"},
        {"player1": "김인환", "player2": "송이헌", "score": "5-1", "winner": "김인환"},
        {"player1": "김인환", "player2": "배준호", "score": "5-2", "winner": "김인환"},
        {"player1": "김인환", "player2": "김태오", "score": "5-0", "winner": "김인환"},
        
        {"player1": "조재찬", "player2": "김인환", "score": "5-4", "winner": "조재찬"},
        {"player1": "조재찬", "player2": "이륜호", "score": "3-5", "winner": "이륜호"},
        {"player1": "조재찬", "player2": "김서준", "score": "5-1", "winner": "조재찬"},
        {"player1": "조재찬", "player2": "송이헌", "score": "5-2", "winner": "조재찬"},
        {"player1": "조재찬", "player2": "배준호", "score": "5-3", "winner": "조재찬"},
        {"player1": "조재찬", "player2": "김태오", "score": "5-2", "winner": "조재찬"},
        
        {"player1": "이륜호", "player2": "김인환", "score": "3-5", "winner": "김인환"},
        {"player1": "이륜호", "player2": "조재찬", "score": "5-3", "winner": "이륜호"},
        {"player1": "이륜호", "player2": "김서준", "score": "5-1", "winner": "이륜호"},
        {"player1": "이륜호", "player2": "송이헌", "score": "4-5", "winner": "송이헌"},
        {"player1": "이륜호", "player2": "배준호", "score": "5-3", "winner": "이륜호"},
        {"player1": "이륜호", "player2": "김태오", "score": "5-0", "winner": "이륜호"},
        
        {"player1": "김서준", "player2": "김인환", "score": "5-2", "winner": "김서준"},
        {"player1": "김서준", "player2": "조재찬", "score": "4-5", "winner": "조재찬"},
        {"player1": "김서준", "player2": "이륜호", "score": "1-5", "winner": "이륜호"},
        {"player1": "김서준", "player2": "송이헌", "score": "5-3", "winner": "김서준"},
        {"player1": "김서준", "player2": "배준호", "score": "5-2", "winner": "김서준"},
        {"player1": "김서준", "player2": "김태오", "score": "5-1", "winner": "김서준"},
        
        {"player1": "송이헌", "player2": "김인환", "score": "1-5", "winner": "김인환"},
        {"player1": "송이헌", "player2": "조재찬", "score": "4-5", "winner": "조재찬"},
        {"player1": "송이헌", "player2": "이륜호", "score": "5-4", "winner": "송이헌"},
        {"player1": "송이헌", "player2": "김서준", "score": "3-5", "winner": "김서준"},
        {"player1": "송이헌", "player2": "배준호", "score": "5-3", "winner": "송이헌"},
        {"player1": "송이헌", "player2": "김태오", "score": "5-2", "winner": "송이헌"},
        
        {"player1": "배준호", "player2": "김인환", "score": "4-5", "winner": "김인환"},
        {"player1": "배준호", "player2": "조재찬", "score": "4-5", "winner": "조재찬"},
        {"player1": "배준호", "player2": "이륜호", "score": "1-5", "winner": "이륜호"},
        {"player1": "배준호", "player2": "김서준", "score": "2-5", "winner": "김서준"},
        {"player1": "배준호", "player2": "송이헌", "score": "3-5", "winner": "송이헌"},
        {"player1": "배준호", "player2": "김태오", "score": "5-1", "winner": "배준호"},
        
        {"player1": "김태오", "player2": "김인환", "score": "0-5", "winner": "김인환"},
        {"player1": "김태오", "player2": "조재찬", "score": "2-5", "winner": "조재찬"},
        {"player1": "김태오", "player2": "이륜호", "score": "0-5", "winner": "이륜호"},
        {"player1": "김태오", "player2": "김서준", "score": "0-5", "winner": "김서준"},
        {"player1": "김태오", "player2": "송이헌", "score": "0-5", "winner": "송이헌"},
        {"player1": "김태오", "player2": "배준호", "score": "1-5", "winner": "배준호"}
      ]
    }
  ]
}
{
  "tournaments": [
    {
      "name": "2022 1월 대한펜싱협회 유소년 국가대표선수 선발전",
      "location": "대한민국",
      "date": "2022-01",
      "division": "유소년",
      "weapon": "Epee",
      "round": "Preliminary",
      "teams": [
        {
          "team_name": "대전탄방중학교",
          "members": [{"name": "길정훈", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "인천체육고등학교",
          "members": [{"name": "최진영", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "덕원중학교",
          "members": [{"name": "차민규", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "서울체육중학교",
          "members": [{"name": "이요한패이글", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "태화중학교",
          "members": [{"name": "박서준", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "남산중학교",
          "members": [{"name": "김규민", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "노스런던컬리지에잇스쿨제주",
          "members": [{"name": "이준영", "weapon": "Epee", "division": "유소년"}]
        }
      ],
      "matches": [
        {"player1": "길정훈", "player2": "최진영", "score": "2-5", "winner": "최진영"},
        {"player1": "길정훈", "player2": "차민규", "score": "4-3", "winner": "길정훈"},
        {"player1": "길정훈", "player2": "이요한패이글", "score": "3-5", "winner": "이요한패이글"},
        {"player1": "길정훈", "player2": "박서준", "score": "5-3", "winner": "길정훈"},
        {"player1": "길정훈", "player2": "김규민", "score": "5-2", "winner": "길정훈"},
        {"player1": "길정훈", "player2": "이준영", "score": "4-3", "winner": "길정훈"},
        
        {"player1": "최진영", "player2": "길정훈", "score": "5-2", "winner": "최진영"},
        {"player1": "최진영", "player2": "차민규", "score": "5-3", "winner": "최진영"},
        {"player1": "최진영", "player2": "이요한패이글", "score": "5-3", "winner": "최진영"},
        {"player1": "최진영", "player2": "박서준", "score": "5-1", "winner": "최진영"},
        {"player1": "최진영", "player2": "김규민", "score": "5-2", "winner": "최진영"},
        {"player1": "최진영", "player2": "이준영", "score": "5-3", "winner": "최진영"},
        
        {"player1": "차민규", "player2": "길정훈", "score": "3-4", "winner": "길정훈"},
        {"player1": "차민규", "player2": "최진영", "score": "3-5", "winner": "최진영"},
        {"player1": "차민규", "player2": "이요한패이글", "score": "2-5", "winner": "이요한패이글"},
        {"player1": "차민규", "player2": "박서준", "score": "5-3", "winner": "차민규"},
        {"player1": "차민규", "player2": "김규민", "score": "5-2", "winner": "차민규"},
        {"player1": "차민규", "player2": "이준영", "score": "5-3", "winner": "차민규"},
        
        {"player1": "이요한패이글", "player2": "길정훈", "score": "5-3", "winner": "이요한패이글"},
        {"player1": "이요한패이글", "player2": "최진영", "score": "4-5", "winner": "최진영"},
        {"player1": "이요한패이글", "player2": "차민규", "score": "5-2", "winner": "이요한패이글"},
        {"player1": "이요한패이글", "player2": "박서준", "score": "5-3", "winner": "이요한패이글"},
        {"player1": "이요한패이글", "player2": "김규민", "score": "5-2", "winner": "이요한패이글"},
        {"player1": "이요한패이글", "player2": "이준영", "score": "5-3", "winner": "이요한패이글"},
        
        {"player1": "박서준", "player2": "길정훈", "score": "4-5", "winner": "길정훈"},
        {"player1": "박서준", "player2": "최진영", "score": "1-5", "winner": "최진영"},
        {"player1": "박서준", "player2": "차민규", "score": "4-5", "winner": "차민규"},
        {"player1": "박서준", "player2": "이요한패이글", "score": "3-5", "winner": "이요한패이글"},
        {"player1": "박서준", "player2": "김규민", "score": "5-3", "winner": "박서준"},
        {"player1": "박서준", "player2": "이준영", "score": "5-3", "winner": "박서준"},
        
        {"player1": "김규민", "player2": "길정훈", "score": "4-5", "winner": "길정훈"},
        {"player1": "김규민", "player2": "최진영", "score": "2-5", "winner": "최진영"},
        {"player1": "김규민", "player2": "차민규", "score": "2-5", "winner": "차민규"},
        {"player1": "김규민", "player2": "이요한패이글", "score": "1-5", "winner": "이요한패이글"},
        {"player1": "김규민", "player2": "박서준", "score": "2-5", "winner": "박서준"},
        {"player1": "김규민", "player2": "이준영", "score": "5-3", "winner": "김규민"},
        
        {"player1": "이준영", "player2": "길정훈", "score": "2-4", "winner": "길정훈"},
        {"player1": "이준영", "player2": "최진영", "score": "2-5", "winner": "최진영"},
        {"player1": "이준영", "player2": "차민규", "score": "3-5", "winner": "차민규"},
        {"player1": "이준영", "player2": "이요한패이글", "score": "4-5", "winner": "이요한패이글"},
        {"player1": "이준영", "player2": "박서준", "score": "5-3", "winner": "이준영"},
        {"player1": "이준영", "player2": "김규민", "score": "4-5", "winner": "김규민"}
      ]
    }
  ]
}
{
  "tournaments": [
    {
      "name": "2022 1월 대한펜싱협회 유소년 국가대표선수 선발전",
      "location": "대한민국",
      "date": "2022-01",
      "division": "유소년",
      "weapon": "Epee",
      "round": "Preliminary",
      "teams": [
        {
          "team_name": "충남체육고등학교",
          "members": [{"name": "정원준", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "진주제일중학교",
          "members": [{"name": "정민욱", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "인천해원중학교",
          "members": [{"name": "박신후", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "덕원중학교",
          "members": [{"name": "이윤제", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "경남체육고등학교",
          "members": [{"name": "오신우", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "대전탄방중학교",
          "members": [{"name": "지민규", "weapon": "Epee", "division": "유소년"}]
        },
        {
          "team_name": "서울체육중학교",
          "members": [{"name": "안리한", "weapon": "Epee", "division": "유소년"}]
        }
      ],
      "matches": [
        {"player1": "정원준", "player2": "정민욱", "score": "5-3", "winner": "정원준"},
        {"player1": "정원준", "player2": "박신후", "score": "3-5", "winner": "박신후"},
        {"player1": "정원준", "player2": "이윤제", "score": "4-5", "winner": "이윤제"},
        {"player1": "정원준", "player2": "오신우", "score": "2-5", "winner": "오신우"},
        {"player1": "정원준", "player2": "지민규", "score": "4-5", "winner": "지민규"},
        {"player1": "정원준", "player2": "안리한", "score": "5-1", "winner": "정원준"},

        {"player1": "정민욱", "player2": "정원준", "score": "3-5", "winner": "정원준"},
        {"player1": "정민욱", "player2": "박신후", "score": "5-3", "winner": "정민욱"},
        {"player1": "정민욱", "player2": "이윤제", "score": "5-3", "winner": "정민욱"},
        {"player1": "정민욱", "player2": "오신우", "score": "3-5", "winner": "오신우"},
        {"player1": "정민욱", "player2": "지민규", "score": "4-5", "winner": "지민규"},
        {"player1": "정민욱", "player2": "안리한", "score": "1-5", "winner": "안리한"},

        {"player1": "박신후", "player2": "정원준", "score": "5-3", "winner": "박신후"},
        {"player1": "박신후", "player2": "정민욱", "score": "3-5", "winner": "정민욱"},
        {"player1": "박신후", "player2": "이윤제", "score": "5-3", "winner": "박신후"},
        {"player1": "박신후", "player2": "오신우", "score": "1-5", "winner": "오신우"},
        {"player1": "박신후", "player2": "지민규", "score": "4-5", "winner": "지민규"},
        {"player1": "박신후", "player2": "안리한", "score": "5-3", "winner": "박신후"},

        {"player1": "이윤제", "player2": "정원준", "score": "5-4", "winner": "이윤제"},
        {"player1": "이윤제", "player2": "정민욱", "score": "3-5", "winner": "정민욱"},
        {"player1": "이윤제", "player2": "박신후", "score": "3-5", "winner": "박신후"},
        {"player1": "이윤제", "player2": "오신우", "score": "1-5", "winner": "오신우"},
        {"player1": "이윤제", "player2": "지민규", "score": "5-3", "winner": "이윤제"},
        {"player1": "이윤제", "player2": "안리한", "score": "5-3", "winner": "이윤제"},

        {"player1": "오신우", "player2": "정원준", "score": "5-2", "winner": "오신우"},
        {"player1": "오신우", "player2": "정민욱", "score": "5-3", "winner": "오신우"},
        {"player1": "오신우", "player2": "박신후", "score": "5-1", "winner": "오신우"},
        {"player1": "오신우", "player2": "이윤제", "score": "5-4", "winner": "오신우"},
        {"player1": "오신우", "player2": "지민규", "score": "3-5", "winner": "지민규"},
        {"player1": "오신우", "player2": "안리한", "score": "5-2", "winner": "오신우"},

        {"player1": "지민규", "player2": "정원준", "score": "5-4", "winner": "지민규"},
        {"player1": "지민규", "player2": "정민욱", "score": "5-4", "winner": "지민규"},
        {"player1": "지민규", "player2": "박신후", "score": "5-3", "winner": "지민규"},
        {"player1": "지민규", "player2": "이윤제", "score": "4-5", "winner": "이윤제"},
        {"player1": "지민규", "player2": "오신우", "score": "3-5", "winner": "오신우"},
        {"player1": "지민규", "player2": "안리한", "score": "5-2", "winner": "지민규"},

        {"player1": "안리한", "player2": "정원준", "score": "1-5", "winner": "정원준"},
        {"player1": "안리한", "player2": "정민욱", "score": "5-3", "winner": "안리한"},
        {"player1": "안리한", "player2": "박신후", "score": "3-5", "winner": "박신후"},
        {"player1": "안리한", "player2": "이윤제", "score": "4-5", "winner": "이윤제"},
        {"player1": "안리한", "player2": "오신우", "score": "3-5", "winner": "오신우"},
        {"player1": "안리한", "player2": "지민규", "score": "5-2", "winner": "안리한"}
      ]
    }
  ]
}


# 선수별 전적 계산
player_stats = calculate_player_stats(tournaments)

# 데이터프레임 변환 및 정렬
df = pd.DataFrame.from_dict(player_stats, orient="index")
df.index.name = "선수 이름"
df.reset_index(inplace=True)
df.sort_values(by=["승률", "승"], ascending=[False, False], inplace=True)

# 데이터 표시
import ace_tools as tools
tools.display_dataframe_to_user(name="펜싱 선수 전적", dataframe=df)
