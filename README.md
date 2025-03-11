{
  "tournaments": [
    {
      "name": "2024 전국 펜싱 대회",
      "location": "서울",
      "date": "2024-06-15",
      "division": "고등부",
      "teams": [
        {
          "team_name": "서울 체고",
          "members": [
            {"name": "홍길동", "weapon": "Foil", "division": "고등부"},
            {"name": "김철수", "weapon": "Sabre", "division": "고등부"}
          ]
        },
        {
          "team_name": "대전체고",
          "members": [
            {"name": "박민수", "weapon": "Epee", "division": "고등부"},
            {"name": "이민호", "weapon": "Foil", "division": "고등부"}
          ]
        }
      ],
      "matches": [
        {
          "round": "Preliminary",
          "weapon": "Foil",
          "division": "고등부",
          "player1": "홍길동",
          "player2": "김철수",
          "score": "5-3",
          "winner": "홍길동"
        },
        {
          "round": "Final",
          "weapon": "Epee",
          "division": "고등부",
          "player1": "박민수",
          "player2": "이민호",
          "score": "15-12",
          "winner": "박민수"
        }
      ]
    }
  ]
}




C++코드
#include <iostream>
#include <fstream>
#include <string>
#include <iomanip>
#include "nlohmann/json.hpp"

using json = nlohmann::json;
using namespace std;

// JSON 데이터 로드 함수
json loadDatabase() {
    ifstream file("data.json");
    if (!file.is_open()) {
        cerr << "❌ 데이터 파일을 찾을 수 없습니다.\n";
        exit(1);
    }
    json db;
    file >> db;
    file.close();
    return db;
}

// 선수의 경기 기록 및 승률 계산
void searchPlayer(json &db, const string &playerName) {
    bool found = false;
    int prelimWins = 0, prelimTotal = 0;
    int finalWins = 0, finalTotal = 0;

    for (auto &tournament : db["tournaments"]) {
        for (auto &match : tournament["matches"]) {
            if (match["player1"] == playerName || match["player2"] == playerName) {
                if (!found) {
                    cout << "🎖 선수: " << playerName << "\n";
                    found = true;
                }
                cout << "🏆 대회: " << tournament["name"] << " (" << match["round"] << ") - " << match["division"] << "\n";
                cout << "   종목: " << match["weapon"] << " | 점수: " << match["score"] << " | 승자: " << match["winner"] << "\n";

                if (match["round"] == "Preliminary") {
                    prelimTotal++;
                    if (match["winner"] == playerName) prelimWins++;
                } else if (match["round"] == "Final") {
                    finalTotal++;
                    if (match["winner"] == playerName) finalWins++;
                }
            }
        }
    }

    if (!found) {
        cout << "❌ 해당 선수를 찾을 수 없습니다.\n";
    } else {
        cout << "========================================\n";
        cout << "📊 승률 분석\n";
        cout << "   예선 승률: " << fixed << setprecision(2)
             << (prelimTotal > 0 ? (prelimWins * 100.0 / prelimTotal) : 0) << "% (" 
             << prelimWins << "/" << prelimTotal << ")\n";
        cout << "   본선 승률: " << fixed << setprecision(2)
             << (finalTotal > 0 ? (finalWins * 100.0 / finalTotal) : 0) << "% (" 
             << finalWins << "/" << finalTotal << ")\n";
    }
}

// 대회 및 팀 정보 검색
void searchTournament(json &db, const string &tournamentName) {
    bool found = false;

    for (auto &tournament : db["tournaments"]) {
        if (tournament["name"] == tournamentName) {
            cout << "🏆 TOURNAMENT NAME: " << tournament["name"] << "\n";
            cout << "📍 Location: " << tournament["location"] << " | 🗓 Date: " << tournament["date"] << "\n";
            cout << "🔹 Division: " << tournament["division"] << "\n";
            cout << "========================================\n";
            cout << "📋 TEAM LIST\n";

            for (auto &team : tournament["teams"]) {
                cout << "🔹 Team: " << team["team_name"] << "\n";
                cout << "   Members:\n";
                int count = 1;
                for (auto &member : team["members"]) {
                    cout << "      (" << count << ") " << member["name"] 
                         << " - 종목: " << member["weapon"]
                         << " - Division: " << member["division"] << "\n";
                    count++;
                }
                cout << "----------------------------------------\n";
            }
            found = true;
            break;
        }
    }

    if (!found) {
        cout << "❌ 해당 대회를 찾을 수 없습니다.\n";
    }
}

int main() {
    setlocale(LC_ALL, ""); // 한글 깨짐 방지
    json db = loadDatabase();

    while (true) {
        string input;
        cout << "\n🔍 대회 검색: 'T' | 선수 검색: 'P' | 종료: 'Q' 입력: ";
        cin >> input;
        cin.ignore();

        if (input == "T") {
            string tournamentName;
            cout << "검색할 대회 이름을 입력하세요: ";
            getline(cin, tournamentName);
            searchTournament(db, tournamentName);
        } else if (input == "P") {
            string playerName;
            cout << "검색할 선수 이름을 입력하세요: ";
            getline(cin, playerName);`
            searchPlayer(db, playerName);
        } else if (input == "Q") {
            cout << "🚪 프로그램을 종료합니다.\n";
            break;
        } else {
            cout << "❌ 잘못된 입력입니다. 다시 시도하세요.\n";
        }
    }
    return 0;
}
