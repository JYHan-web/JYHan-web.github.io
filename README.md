package com.fencing.stats;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

import java.util.*;
import java.util.stream.Collectors;

@SpringBootApplication
public class FencerStatsApp {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        SpringApplication.run(FencerStatsApp.class, args);

        FencerRepository repo = new FencerRepository();
        repo.populateSampleMatches();

        // 사용자 입력을 통해 특정 선수 전적 조회
        System.out.println("\n확인할 선수 이름을 입력하세요:");
        String inputName = scanner.nextLine();
        System.out.println("\n=== [" + inputName + "] 선수 전적 ===");
        repo.printFencerStats(inputName);

        // 전체 전적 출력
        for (Match match : repo.getAllMatches()) {
            System.out.println(match);
        }
    }
}

class Fencer {
    String name;
    String team;
    int wins = 0;
    int losses = 0;

    public Fencer(String name, String team) {
        this.name = name;
        this.team = team;
    }

    public void addWin() {
        wins++;
    }

    public void addLoss() {
        losses++;
    }

    // 승률 계산. 소숫점 둘째 자리까지 반올림
    public double getWinRate() {
        int total = wins + losses;
        return total == 0 ? 0.0 : Math.round((wins * 10000.0 / total)) / 100.0;
    }

    @Override
    public String toString() {
        return String.format("%s (%s): %d승 %d패, 승률 %.2f%%",
                name, team, wins, losses, getWinRate());
    }
}

class Match {
    String tournament;
    Fencer winner;
    Fencer loser;
    int winnerScore;
    int loserScore;

    public Match(String tournament, Fencer winner, Fencer loser, int winnerScore, int loserScore) {
        this.tournament = tournament;
        this.winner = winner;
        this.loser = loser;
        this.winnerScore = winnerScore;
        this.loserScore = loserScore;
    }

    @Override
    public String toString() {
        return String.format("[%s] %s %d:%d %s",
                tournament, winner.name, winnerScore, loserScore, loser.name);
    }
}

class FencerRepository {
    Map<String, Fencer> fencerMap = new HashMap<>(); // 이름으로 펜싱 선수 객체 관리
    List<Match> matches = new ArrayList<>(); // 경기 전적 저장 리스트

    // 선수 객체를 이름 기준으로 조회하거나 없으면 새로 생성
    public Fencer getOrCreate(String name, String team) {
        if (!fencerMap.containsKey(name)) {
            fencerMap.put(name, new Fencer(name, team));
        }
        return fencerMap.get(name);
    }

    // 경기 결과를 기록하고, 선수의 승패를 갱신
    public void recordMatch(String winnerName, String winnerTeam, int winnerScore,
                            String loserName, String loserTeam, int loserScore,
                            String tournament) {
        Fencer winner = getOrCreate(winnerName, winnerTeam);
        Fencer loser = getOrCreate(loserName, loserTeam);
        matches.add(new Match(tournament, winner, loser, winnerScore, loserScore));
        winner.addWin();
        loser.addLoss();
    }

    public List<Fencer> getAllFencers() {
        return new ArrayList<>(fencerMap.values());
    }

    public List<Match> getAllMatches() {
        return matches;
    }

    // 특정 선수의 전적을 출력
    public void printFencerStats(String fencerName) {
        List<Match> related = matches.stream()
                .filter(m -> m.winner.name.equals(fencerName) || m.loser.name.equals(fencerName))
                .collect(Collectors.toList());
        if (related.isEmpty()) {
            System.out.println(fencerName + " 선수의 전적이 없습니다.");
            return;
        }
        for (Match m : related) {
            System.out.println(m);
        }
        Fencer f = fencerMap.get(fencerName);
        if (f != null) {
            System.out.println("\n총 전적: " + f);
        }
    }

    // 경기 데이터 삽입용 더미 함수 (생략)
    public void populateSampleMatches() {
        String t1 = "2022년 1월 유소년 국가대표 선발전 - 1뿔";
        recordMatch("고동연", "하길중학교", 5, "김휘성", "상안중학교", 1, t1);
        recordMatch("조희윤", "인천해원중학교", 5, "김휘성", "상안중학교", 4, t1);
        recordMatch("김태형", "동탄펜싱클럽", 5, "김휘성", "상안중학교", 2, t1);
        recordMatch("엄선한", "대전탄방중학교", 5, "김휘성", "상안중학교", 1, t1);
        recordMatch("이민서", "서울체육중학교", 5, "김휘성", "상안중학교", 2, t1);
        recordMatch("고동연", "하길중학교", 5, "조희윤", "인천해원중학교", 3, t1);
        recordMatch("고동연", "하길중학교", 5, "김태형", "동탄펜싱클럽", 4, t1);
        recordMatch("고동연", "하길중학교", 5, "엄선한", "대전탄방중학교", 2, t1);
        recordMatch("고동연", "하길중학교", 5, "이민서", "서울체육중학교", 3, t1);
        recordMatch("김태형", "동탄펜싱클럽", 5, "조희윤", "인천해원중학교", 3, t1);
        recordMatch("조희윤", "인천해원중학교", 5, "엄선한", "대전탄방중학교", 2, t1);
        recordMatch("이민서", "서울체육중학교", 5, "조희윤", "인천해원중학교", 0, t1);
        recordMatch("엄선한", "대전탄방중학교", 5, "김태형", "동탄펜싱클럽", 4, t1);
        recordMatch("이민서", "서울체육중학교", 5, "김태형", "동탄펜싱클럽", 0, t1);
        recordMatch("이민서", "서울체육중학교", 5, "엄선한", "대전탄방중학교", 3, t1);

        String t2 = "2022년 1월 유소년 국가대표 선발전 - 2뿔";
        recordMatch("김민성", "진주제일중학교", 5, "김무현", "중경고등학교", 4, t2);
        recordMatch("김성수", "부산체육고등학교", 5, "김무현", "중경고등학교", 4, t2);
        recordMatch("김무현", "중경고등학교", 5, "이도협", "해남제일중", 4, t2);
        recordMatch("김무현", "중경고등학교", 5, "권윤찬", "서울체육중", 2, t2);
        recordMatch("김무현", "중경고등학교", 5, "한건희", "익산부천중학교", 2, t2);
        recordMatch("김무현", "중경고등학교", 5, "정은수", "대전탄방중학교", 1, t2);
        recordMatch("김민성", "진주제일중학교", 5, "김성수", "부산체육고등학교", 2, t2);
        recordMatch("김민성", "진주제일중학교", 5, "이도협", "해남제일중", 3, t2);
        recordMatch("김민성", "진주제일중학교", 5, "권윤찬", "서울체육중", 4, t2);
        recordMatch("김민성", "진주제일중학교", 5, "한건희", "익산부천중학교", 3, t2);
        recordMatch("김민성", "진주제일중학교", 5, "정은수", "대전탄방중학교", 0, t2);
        recordMatch("이도협", "해남제일중", 5, "김성수", "부산체육고등학교", 3, t2);
        recordMatch("김성수", "부산체육고등학교", 5, "권윤찬", "서울체육중", 4, t2);
        recordMatch("김성수", "부산체육고등학교", 5, "한건희", "익산부천중학교", 3, t2);
        recordMatch("정은수", "대전탄방중학교", 5, "김성수", "부산체육고등학교", 2, t2);
        recordMatch("권윤찬", "서울체육중", 5, "이도협", "해남제일중", 4, t2);
        recordMatch("이도협", "해남제일중", 5, "한건희", "익산부천중학교", 2, t2);
        recordMatch("정은수", "대전탄방중학교", 5, "이도협", "해남제일중", 4, t2);
        recordMatch("한건희", "익산부천중학교", 5, "권윤찬", "서울체육중", 3, t2);
        recordMatch("정은수", "대전탄방중학교", 5, "권윤찬", "서울체육중", 3, t2);
        recordMatch("정은수", "대전탄방중학교", 5, "한건희", "익산부천중학교", 3, t2);

        String t3 = "2022년 1월 유소년 국가대표 선발전 - 3뿔";
        recordMatch("윤영도", "서울체육중학교", 5, "김승범", "경남체육고등학교", 1, t3);
        recordMatch("김승범", "경남체육고등학교", 5, "박효렬", "전북체육고등학교", 0, t3);
        recordMatch("김승범", "경남체육고등학교", 5, "이준현", "태화중학교", 0, t3);
        recordMatch("최정휴", "진주제일중학교", 5, "김승범", "경남체육고등학교", 4, t3);
        recordMatch("김승범", "경남체육고등학교", 5, "윙베르윌리암가브리엘", "대전펜싱클럽", 0, t3);
        recordMatch("김승범", "경남체육고등학교", 5, "이민승", "대전탄방중학교", 0, t3);
        recordMatch("윤영도", "서울체육중학교", 5, "박효렬", "전북체육고등학교", 4, t3);
        recordMatch("이준현", "태화중학교", 5, "윤영도", "서울체육중학교", 1, t3);
        recordMatch("윤영도", "서울체육중학교", 5, "최정휴", "진주제일중학교", 3, t3);
        recordMatch("윤영도", "서울체육중학교", 5, "윙베르윌리암가브리엘", "대전펜싱클럽", 0, t3);
        recordMatch("윤영도", "서울체육중학교", 5, "이민승", "대전탄방중학교", 0, t3);
        recordMatch("박효렬", "전북체육고등학교", 5, "이준현", "태화중학교", 3, t3);
        recordMatch("박효렬", "전북체육고등학교", 5, "최정휴", "진주제일중학교", 2, t3);
        recordMatch("박효렬", "전북체육고등학교", 5, "윙베르윌리암가브리엘", "대전펜싱클럽", 2, t3);
        recordMatch("박효렬", "전북체육고등학교", 5, "이민승", "대전탄방중학교", 2, t3);
        recordMatch("이준현", "태화중학교", 5, "최정휴", "진주제일중학교", 1, t3);
        recordMatch("이준현", "태화중학교", 5, "윙베르윌리암가브리엘", "대전펜싱클럽", 0, t3);
        recordMatch("이준현", "태화중학교", 5, "이민승", "대전탄방중학교", 0, t3);
        recordMatch("최정휴", "진주제일중학교", 5, "윙베르윌리암가브리엘", "대전펜싱클럽", 0, t3);
        recordMatch("최정휴", "진주제일중학교", 5, "이민승", "대전탄방중학교", 0, t3);
        recordMatch("윙베르윌리암가브리엘", "대전펜싱클럽", 5, "이민승", "대전탄방중학교", 3, t3);

        String t4 = "2022년 1월 유소년 국가대표 선발전 - 4뿔";
        recordMatch("김태민", "중경고등학교", 5, "최찬영", "동탄펜싱클럽", 5, t4);
        recordMatch("김태민", "중경고등학교", 5, "김동원", "대전문정중학교", 3, t4);
        recordMatch("김태민", "중경고등학교", 3, "김민재", "남산중학교", 5, t4);
        recordMatch("김태민", "중경고등학교", 0, "한지윤", "은호펜싱클럽", 5, t4);
        recordMatch("김태민", "중경고등학교", 3, "정연우", "대전펜싱클럽", 5, t4);
        recordMatch("오연수", "해남공업고등학교", 3, "김태민", "중경고등학교", 5, t4);
        recordMatch("오연수", "해남공업고등학교", 5, "최찬영", "동탄펜싱클럽", 5, t4);
        recordMatch("김동원", "대전문정중학교", 5, "오연수", "해남공업고등학교", 2, t4);
        recordMatch("김민재", "남산중학교", 5, "오연수", "해남공업고등학교", 1, t4);
        recordMatch("한지윤", "은호펜싱클럽", 5, "오연수", "해남공업고등학교", 2, t4);
        recordMatch("정연우", "대전펜싱클럽", 5, "오연수", "해남공업고등학교", 5, t4);
        recordMatch("김동원", "대전문정중학교", 5, "최찬영", "동탄펜싱클럽", 2, t4);
        recordMatch("김민재", "남산중학교", 5, "최찬영", "동탄펜싱클럽", 1, t4);
        recordMatch("한지윤", "은호펜싱클럽", 5, "최찬영", "동탄펜싱클럽", 3, t4);
        recordMatch("정연우", "대전펜싱클럽", 5, "최찬영", "동탄펜싱클럽", 5, t4);
        recordMatch("김민재", "남산중학교", 5, "김동원", "대전문정중학교", 1, t4);
        recordMatch("김민재", "남산중학교", 5, "한지윤", "은호펜싱클럽", 3, t4);
        recordMatch("김민재", "남산중학교", 5, "정연우", "대전펜싱클럽", 5, t4);
        recordMatch("한지윤", "은호펜싱클럽", 5, "김동원", "대전문정중학교", 2, t4);
        recordMatch("정연우", "대전펜싱클럽", 5, "김동원", "대전문정중학교", 2, t4);
        recordMatch("정연우", "대전펜싱클럽", 5, "한지윤", "은호펜싱클럽", 2, t4);

        String t5 = "2022년 1월 유소년 국가대표 선발전 - 5뿔";
        recordMatch("김새힘", "전북체육고등학교", 5, "김희찬", "대전탄방중학교", 4, t5);
        recordMatch("안무진", "부산체육고등학교", 5, "김희찬", "대전탄방중학교", 0, t5);
        recordMatch("이규한", "진주제일중학교", 5, "김희찬", "대전탄방중학교", 0, t5);
        recordMatch("이상성", "태화중학교", 5, "김희찬", "대전탄방중학교", 0, t5);
        recordMatch("김성보", "덕원중학교", 5, "김희찬", "대전탄방중학교", 0, t5);
        recordMatch("이준우", "", 5, "김희찬", "대전탄방중학교", 0, t5);
        recordMatch("김새힘", "전북체육고등학교", 5, "안무진", "부산체육고등학교", 0, t5);
        recordMatch("김새힘", "전북체육고등학교", 5, "이규한", "진주제일중학교", 2, t5);
        recordMatch("김새힘", "전북체육고등학교", 5, "이상성", "태화중학교", 5, t5);
        recordMatch("김새힘", "전북체육고등학교", 5, "김성보", "덕원중학교", 0, t5);
        recordMatch("김새힘", "전북체육고등학교", 5, "이준우", "", 0, t5);
        recordMatch("안무진", "부산체육고등학교", 5, "이규한", "진주제일중학교", 4, t5);
        recordMatch("안무진", "부산체육고등학교", 5, "이상성", "태화중학교", 4, t5);
        recordMatch("안무진", "부산체육고등학교", 5, "김성보", "덕원중학교", 0, t5);
        recordMatch("안무진", "부산체육고등학교", 5, "이준우", "", 0, t5);
        recordMatch("이규한", "진주제일중학교", 5, "이상성", "태화중학교", 1, t5);
        recordMatch("이규한", "진주제일중학교", 5, "김성보", "덕원중학교", 0, t5);
        recordMatch("이규한", "진주제일중학교", 5, "이준우", "", 0, t5);
        recordMatch("이상성", "태화중학교", 5, "김성보", "덕원중학교", 4, t5);
        recordMatch("이상성", "태화중학교", 5, "이준우", "", 0, t5);
        recordMatch("김성보", "덕원중학교", 5, "이준우", "", 0, t5);

        String t6 = "2022년 1월 유소년 국가대표 선발전 - 6뿔";
        recordMatch("김찬현", "인천해원중학교", 5, "전유섭", "진주제일중학교", 0, t6);
        recordMatch("김찬현", "인천해원중학교", 5, "이지성", "부산체육고등학교", 0, t6);
        recordMatch("김재원", "태화중학교", 5, "김찬현", "인천해원중학교", 0, t6);
        recordMatch("김찬현", "인천해원중학교", 5, "김재원", "상안중학교", 0, t6);
        recordMatch("김찬현", "인천해원중학교", 5, "이동현", "서울체육중학교", 0, t6);
        recordMatch("김찬현", "인천해원중학교", 5, "조이준", "동탄펜싱클럽", 0, t6);
        recordMatch("이지성", "부산체육고등학교", 5, "전유섭", "진주제일중학교", 4, t6);
        recordMatch("전유섭", "진주제일중학교", 5, "김재원", "태화중학교", 3, t6);
        recordMatch("전유섭", "진주제일중학교", 5, "김재원", "상안중학교", 0, t6);
        recordMatch("전유섭", "진주제일중학교", 5, "이동현", "서울체육중학교", 0, t6);
        recordMatch("전유섭", "진주제일중학교", 5, "조이준", "동탄펜싱클럽", 0, t6);
        recordMatch("김재원", "태화중학교", 5, "이지성", "부산체육고등학교", 4, t6);
        recordMatch("김재원", "태화중학교", 5, "김재원", "상안중학교", 4, t6);
        recordMatch("김재원", "태화중학교", 5, "이동현", "서울체육중학교", 0, t6);
        recordMatch("김재원", "태화중학교", 5, "조이준", "동탄펜싱클럽", 0, t6);
        recordMatch("김재원", "상안중학교", 5, "이지성", "부산체육고등학교", 1, t6);
        recordMatch("김재원", "상안중학교", 5, "이동현", "서울체육중학교", 2, t6);
        recordMatch("김재원", "상안중학교", 5, "조이준", "동탄펜싱클럽", 2, t6);
        recordMatch("이동현", "서울체육중학교", 5, "이지성", "부산체육고등학교", 2, t6);
        recordMatch("이동현", "서울체육중학교", 5, "조이준", "동탄펜싱클럽", 2, t6);
        recordMatch("조이준", "동탄펜싱클럽", 5, "이지성", "부산체육고등학교", 2, t6);

        String t7 = "2022년 1월 유소년 국가대표 선발전 - 7뿔";
        recordMatch("정수민", "진주제일중학교", 5, "주성연", "광주체육고등학교", 2, t7);
        recordMatch("주성연", "광주체육고등학교", 5, "박지민", "광주체육고등학교", 0, t7);
        recordMatch("주성연", "광주체육고등학교", 5, "이윤재", "서울체육중학교", 0, t7);
        recordMatch("주성연", "광주체육고등학교", 5, "조범진", "태화중학교", 0, t7);
        recordMatch("김정식", "덕원중학교", 5, "주성연", "광주체육고등학교", 4, t7);
        recordMatch("주성연", "광주체육고등학교", 5, "이은파", "동탄펜싱클럽", 0, t7);
        recordMatch("정수민", "진주제일중학교", 5, "박지민", "광주체육고등학교", 4, t7);
        recordMatch("정수민", "진주제일중학교", 5, "이윤재", "서울체육중학교", 0, t7);
        recordMatch("정수민", "진주제일중학교", 5, "조범진", "태화중학교", 0, t7);
        recordMatch("정수민", "진주제일중학교", 5, "김정식", "덕원중학교", 0, t7);
        recordMatch("정수민", "진주제일중학교", 5, "이은파", "동탄펜싱클럽", 0, t7);
        recordMatch("박지민", "광주체육고등학교", 5, "이윤재", "서울체육중학교", 0, t7);
        recordMatch("박지민", "광주체육고등학교", 5, "조범진", "태화중학교", 0, t7);
        recordMatch("박지민", "광주체육고등학교", 5, "김정식", "덕원중학교", 0, t7);
        recordMatch("박지민", "광주체육고등학교", 5, "이은파", "동탄펜싱클럽", 0, t7);
        recordMatch("이윤재", "서울체육중학교", 5, "조범진", "태화중학교", 0, t7);
        recordMatch("이윤재", "서울체육중학교", 5, "김정식", "덕원중학교", 0, t7);
        recordMatch("이윤재", "서울체육중학교", 5, "이은파", "동탄펜싱클럽", 0, t7);
        recordMatch("조범진", "태화중학교", 5, "김정식", "덕원중학교", 0, t7);
        recordMatch("조범진", "태화중학교", 5, "이은파", "동탄펜싱클럽", 0, t7);
        recordMatch("김정식", "덕원중학교", 5, "이은파", "동탄펜싱클럽", 0, t7);

        String t8 = "2022년 1월 유소년 국가대표 선발전 - 8뿔";
        recordMatch("김현빈", "부산체육고등학교", 5, "김내훈", "인천해원중학교", 3, t8);
        recordMatch("서현준", "광주체육고등학교", 5, "김내훈", "인천해원중학교", 4, t8);
        recordMatch("김내훈", "인천해원중학교", 5, "조용진", "두암중학교", 0, t8);
        recordMatch("김내훈", "인천해원중학교", 5, "오정민", "진주제일중학교", 0, t8);
        recordMatch("김민서", "하길중학교", 5, "김내훈", "인천해원중학교", 4, t8);
        recordMatch("김내훈", "인천해원중학교", 5, "반승수", "대전탄방중학교", 0, t8);
        recordMatch("김현빈", "부산체육고등학교", 5, "서현준", "광주체육고등학교", 4, t8);
        recordMatch("김현빈", "부산체육고등학교", 5, "조용진", "두암중학교", 0, t8);
        recordMatch("김현빈", "부산체육고등학교", 5, "오정민", "진주제일중학교", 0, t8);
        recordMatch("김현빈", "부산체육고등학교", 5, "김민서", "하길중학교", 0, t8);
        recordMatch("김현빈", "부산체육고등학교", 5, "반승수", "대전탄방중학교", 0, t8);
        recordMatch("서현준", "광주체육고등학교", 5, "조용진", "두암중학교", 0, t8);
        recordMatch("서현준", "광주체육고등학교", 5, "오정민", "진주제일중학교", 0, t8);
        recordMatch("서현준", "광주체육고등학교", 5, "김민서", "하길중학교", 0, t8);
        recordMatch("서현준", "광주체육고등학교", 5, "반승수", "대전탄방중학교", 0, t8);
        recordMatch("조용진", "두암중학교", 5, "오정민", "진주제일중학교", 4, t8);
        recordMatch("김민서", "하길중학교", 5, "조용진", "두암중학교", 0, t8);
        recordMatch("반승수", "대전탄방중학교", 5, "조용진", "두암중학교", 0, t8);
        recordMatch("김민서", "하길중학교", 5, "오정민", "진주제일중학교", 0, t8);
        recordMatch("반승수", "대전탄방중학교", 5, "오정민", "진주제일중학교", 0, t8);
        recordMatch("김민서", "하길중학교", 5, "반승수", "대전탄방중학교", 0, t8);

        String t9 = "2022년 1월 유소년 국가대표 선발전 - 9뿔";
        recordMatch("김민욱", "불곡고등학교", 5, "김준수", "인천해원중학교", 2, t9);
        recordMatch("전수범", "광주체육중학교", 5, "김준수", "인천해원중학교", 2, t9);
        recordMatch("김태환", "계룡중학교", 5, "김준수", "인천해원중학교", 3, t9);
        recordMatch("김민준", "태화중학교", 5, "김준수", "인천해원중학교", 4, t9);
        recordMatch("김성준", "남산중학교", 5, "김준수", "인천해원중학교", 3, t9);
        recordMatch("안시언", "상안중학교", 5, "김준수", "인천해원중학교", 0, t9);
        recordMatch("김민욱", "불곡고등학교", 5, "전수범", "광주체육중학교", 2, t9);
        recordMatch("김민욱", "불곡고등학교", 5, "김태환", "계룡중학교", 2, t9);
        recordMatch("김민욱", "불곡고등학교", 5, "김민준", "태화중학교", 2, t9);
        recordMatch("김민욱", "불곡고등학교", 5, "김성준", "남산중학교", 3, t9);
        recordMatch("김민욱", "불곡고등학교", 5, "안시언", "상안중학교", 4, t9);
        recordMatch("전수범", "광주체육중학교", 5, "김태환", "계룡중학교", 3, t9);
        recordMatch("전수범", "광주체육중학교", 5, "김민준", "태화중학교", 3, t9);
        recordMatch("전수범", "광주체육중학교", 5, "김성준", "남산중학교", 2, t9);
        recordMatch("전수범", "광주체육중학교", 5, "안시언", "상안중학교", 1, t9);
        recordMatch("김태환", "계룡중학교", 5, "김민준", "태화중학교", 2, t9);
        recordMatch("김태환", "계룡중학교", 5, "김성준", "남산중학교", 1, t9);
        recordMatch("김태환", "계룡중학교", 5, "안시언", "상안중학교", 1, t9);
        recordMatch("김민준", "태화중학교", 5, "김성준", "남산중학교", 0, t9);
        recordMatch("김민준", "태화중학교", 5, "안시언", "상안중학교", 4, t9);
        recordMatch("김성준", "남산중학교", 5, "안시언", "상안중학교", 3, t9);

        String t10 = "2022년 1월 유소년 국가대표 선발전 - 10뿔";
        recordMatch("조재찬", "불곡고등학교", 5, "김인환", "인천체육고등학교", 4, t10);
        recordMatch("김인환", "인천체육고등학교", 5, "이륜호", "계룡중학교", 5, t10);
        recordMatch("김서준", "서울체육중학교", 5, "김인환", "인천체육고등학교", 2, t10);
        recordMatch("김인환", "인천체육고등학교", 5, "송이헌", "태화중학교", 5, t10);
        recordMatch("김인환", "인천체육고등학교", 5, "배준호", "부산체육고등학교", 5, t10);
        recordMatch("김인환", "인천체육고등학교", 5, "김태오", "인천해원중학교", 5, t10);
        recordMatch("조재찬", "불곡고등학교", 5, "이륜호", "계룡중학교", 3, t10);
        recordMatch("조재찬", "불곡고등학교", 5, "김서준", "서울체육중학교", 5, t10);
        recordMatch("조재찬", "불곡고등학교", 5, "송이헌", "태화중학교", 5, t10);
        recordMatch("조재찬", "불곡고등학교", 5, "배준호", "부산체육고등학교", 5, t10);
        recordMatch("조재찬", "불곡고등학교", 5, "김태오", "인천해원중학교", 5, t10);

        String t11 = "2022년 1월 유소년 국가대표 선발전 - 11뿔";
        recordMatch("최진영", "인천체육고등학교", 5, "길정훈", "대전탄방중학교", 2, t11);
        recordMatch("길정훈", "대전탄방중학교", 5, "차민규", "덕원중학교", 4, t11);
        recordMatch("이요한패이글", "서울체육중학교", 5, "길정훈", "대전탄방중학교", 3, t11);
        recordMatch("길정훈", "대전탄방중학교", 5, "박서준", "태화중학교", 5, t11);
        recordMatch("길정훈", "대전탄방중학교", 5, "김규민", "남산중학교", 5, t11);
        recordMatch("길정훈", "대전탄방중학교", 5, "이준영", "노스런던컬리지에잇스쿨제주", 4, t11);
        recordMatch("최진영", "인천체육고등학교", 5, "차민규", "덕원중학교", 5, t11);
        recordMatch("최진영", "인천체육고등학교", 5, "이요한패이글", "서울체육중학교", 5, t11);
        recordMatch("최진영", "인천체육고등학교", 5, "박서준", "태화중학교", 5, t11);
        recordMatch("최진영", "인천체육고등학교", 5, "김규민", "남산중학교", 5, t11);
        recordMatch("최진영", "인천체육고등학교", 5, "이준영", "노스런던컬리지에잇스쿨제주", 5, t11);

        String t12 = "2022년 1월 유소년 국가대표 선발전 - 12뿔";
        recordMatch("정민욱", "진주제일중학교", 5, "정원준", "충남체육고등학교", 3, t12);
        recordMatch("정원준", "충남체육고등학교", 5, "박신후", "인천해원중학교", 3, t12);
        recordMatch("이윤제", "덕원중학교", 5, "정원준", "충남체육고등학교", 4, t12);
        recordMatch("정원준", "충남체육고등학교", 5, "오신우", "경남체육고등학교", 2, t12);
        recordMatch("정원준", "충남체육고등학교", 5, "지민규", "대전탄방중학교", 4, t12);
        recordMatch("정원준", "충남체육고등학교", 5, "안리한", "서울체육중학교", 5, t12);
        recordMatch("정민욱", "진주제일중학교", 5, "박신후", "인천해원중학교", 5, t12);
        recordMatch("정민욱", "진주제일중학교", 5, "이윤제", "덕원중학교", 5, t12);
        recordMatch("정민욱", "진주제일중학교", 5, "오신우", "경남체육고등학교", 3, t12);
        recordMatch("정민욱", "진주제일중학교", 5, "지민규", "대전탄방중학교", 4, t12);
        recordMatch("정민욱", "진주제일중학교", 5, "안리한", "서울체육중학교", 1, t12);
        
    }
}
