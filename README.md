import requests
from bs4 import BeautifulSoup



for k in ['mon', 'tue','wed','thu','fri','sat','sun']:

    res = requests.get(f"https://comic.naver.com/webtoon/weekdayList?week={k}")
    soup = BeautifulSoup(res.text, "html.parser")

    for i in soup.select(".thumb > a"):
        titleid = i.get("href").split("=")[1].split("&")[0]

        res = requests.get(f"https://comic.naver.com/webtoon/list?titleId={titleid}")
        soup = BeautifulSoup(res.text, "html.parser")

        print("="*30)
        print(soup.select_one("h2 > .title").text)
        print("="*30)
        print(f'작가\t{soup.select_one(".wrt_nm").text.strip()}')
        print(f'장르\t{soup.select_one(".genre").text}')
        print(f'연령\t{soup.select_one(".age").text}')
        print("="*30)
        print(soup.select_one(".detail > p").text)
        print()
        print()
