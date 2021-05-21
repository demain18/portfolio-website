<template>
  <div>
    <div id="app">
      <div id="gnb">
        <div class="background"></div>
        <h2>Baeksan's Website</h2>
        <div class="profile">
          <div class="circle"></div>
        </div>

        <div class="lang" @click="langSelectClick">
          <img :src="require(`~/assets/img/flag-${lang.flagName[lang.set]}.png`)">
          <span>{{ lang.list[lang.set] }}</span>
          <select v-model="lang.set" class="select">
            <option v-for="(item, index) in lang.list" :key="index" :value="index">
              {{ item }}
            </option>
          </select>
        </div>

      </div>
      <div id="container">
        <div class="profile">

          <h2 v-if="lang.set==0">김명준</h2>
          <h2 v-else-if="lang.set==1">Myoung Joon Kim</h2>
          <h2 v-else-if="lang.set==2">キム・ミョンジュン</h2>

          <p class="intro" v-if="lang.set==0">풀스택 개발자</p>
          <p class="intro" v-else-if="lang.set==1">Fullstack Engineer</p>
          <p class="intro" v-else-if="lang.set==2">フルスタックエンジニア</p>

          <div class="links">
            <p>
              <img src="~assets/img/icon/icon-github.png">
              <a href="https://github.com/demain18" target="_blank">github.com/dylan</a></p>
            <p>
              <img src="~assets/img/icon/icon-insta-dark.png">
              <a href="https://www.instagram.com/baeksan01/" target="_blank">instagram.com/baeksan</a>
            </p>
            <p>
              <img src="~assets/img/icon/icon-book.png">
              <a href="https://demain18-blog.tistory.com/" target="_blank">baeksan.tistory.blog</a>
            </p><br />
            <p>
              <img src="~assets/img/icon/icon-mail.png">
              happysugar180@gmail.com
            </p>
            <div class="map-grid" @mouseover="eventHoverIn" @mouseleave="eventHoverOut">
              <div class="map" :class="{ onDisplay: event.hover }">
                <div class="box">
                  <img src="~assets/img/google-map-ex.png" alt="">
                </div>
              </div>
              <img src="~assets/img/icon/icon-map-point.png">
              Republic of Korea, Seoul
            </div>
          </div>
        </div>

        <div class="section">
          <h2 class="header">About Me</h2>
          <div v-if="lang.set==0">
            <p class="content">
              안녕하세요. 풀스택 개발자로 활동하고 있는 김명준입니다. <br />
              가지고 있는 아이디어를 웹 어플리케이션으로 만들어내는 일을 즐기며 그 과정에서 얻는 성취감을 좋아합니다.<br />
              작은 규모에서 시작해서 사용자가 늘어나며 생태계가 생기고 서비스가 성장하는 모습을 보는것이 제가 개발을 하는 이유입니다.
            </p>
            <p class="content">
              본업은 개발이지만 이외에도 작곡나 글쓰기와 같은 취미가 있으며<br />
              다른 분야에서도 작품을 만들어 사람들에게 저만의 감성을 전하고자 합니다.<br />
              모든 활동은 블로그나 인스타그램에서 진행되고 있으니 많은 관심 가져주세요!
            </p>
          </div>
          <div v-if="lang.set==1">
            <p class="content">
              Hello, I’m myoung joon kim, a full-stack engineer.<br />
              I am really enthusiastic about transformimng my ideas into web application, and also fully enjoy accomplishment acquired in the course of it. <br />
              Starting from a small scale, seeing a growth of users, eco-systems are created and services evolve really motivates me.
            </p>
            <p class="content">  
              Other than my main job as IT engineer, I have hobbies such as composing and writing, because<br />
              I also hope to emotionally attract people with my own unique  sense through works at other fields.<br />
              All the activities are on my blogs and Instagram, so your attention would be so thanked.
            </p>
          </div>
          <div v-if="lang.set==2">
            <p class="content">
              こんにちは。私はフルスタック.エンジニアのミョンジュンキムです。<br />
              私はウェブアプリケーションを通じてアイデアを生み出すのが好きで、その過程から得られる達成感が好きです。<br />
              小さい規模から始めてユーザが増えて生態系ができてサービスが成長するを見るのが私が開発する理由です。
            </p>
            <p class="content">
              私の主な仕事は開発ですが,作曲や執筆などの趣味もあります。<br />
              私は他の分野の作品を作り,自分の感情を人々に伝えたい。<br />
              すべての活動はブログやインスタグラムで行われていますので、多くの関心をお願いします！
            </p>
          </div>
        </div>

        <div class="section">
          <h2 class="header">Skills</h2>
          <div class="list">
            <div class="item"><img src="~assets/img/stack/stack-nuxt.png"></div>
            <div class="item"><img src="~assets/img/stack/stack-codeigniter.png"></div>
            <div class="item"><img src="~assets/img/stack/stack-docker.png"></div>
            <div class="item"><img src="~assets/img/stack/stack-aws.png"></div>
          </div>
        </div>
      </div>

      <div id="project">
        <h2 class="header">Projects</h2>
        <div class="flex">
          <div v-for="(item, index) in projectList.items" :key="index" 
            @mouseover="projectContentToggle('in', index)"
            @mouseleave="projectContentToggle('out', index)"
            @click="dialogToggle(index)" class="item-grid"
          >
            <img :src="require(`~/assets/img/upload/${item.folderName}/1.png`)" alt="">
            <div class="item" :class="{gradient: item.contentToggle}">
              <div class="table">
                <p>{{ item.content.title }}</p>
                <p>{{ item.content.category }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>

      <v-dialog v-model="dialog.on" @click:outside="dialogClose(dialog.index)" width="1200">
        <v-card>
          <v-card-text>
            <div class="content">
              <h2>{{ projectList.items[dialog.index].content.title }}</h2>
              <p>{{ projectList.items[dialog.index].content.category }}</p>
              <a v-if="projectList.items[dialog.index].content.link!=null" :href="projectList.items[dialog.index].content.link" target="_blank"><v-icon>mdi-earth</v-icon></a>
              <a v-if="projectList.items[dialog.index].content.github!=null" :href="projectList.items[dialog.index].content.github" target="_blank"><v-icon>mdi-github</v-icon></a>
              <div class="chip-wrap">
                <v-chip v-for="(item, index) in projectList.items[dialog.index].content.stack" :key="index">{{ item }}</v-chip>
              </div>
            </div>
          </v-card-text>
          <v-card-text>
            <img
              v-for="(item, index) in projectList.items[dialog.index].imgCount" 
              :key="index" 
              :src="require(`~/assets/img/upload/${projectList.items[dialog.index].folderName}/${item}.png`)" 
            >
          </v-card-text>
        </v-card>
      </v-dialog>

      <div id="footer">
        <strong>ⓒ Co.Infinia, All rights reserved.</strong>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data: () => ({
      lang: {
        list: [
          '한국어',
          'English',
          '日本語'
        ],
        flagName: [
          'kor',
          'eng',
          'jp'
        ],
        set: 0
      },
      event: {
        hover: false
      },
      projectList: {
        items: [
          {
            contentToggle: false,
            folderName: 'wehobby',
            imgCount: 5,
            content: {
              title: '위하비(WeHobby)',
              category: '개인 프로젝트',
              link: 'https://www.wehobby.kr/',
              github: 'https://github.com/demain18/wehobby-client',
              stack: [
                'Vue.js', 'Nuxt.js', 'Codeigniter', 'Mysql', 'AWS', 'Prometheus'
              ]
            }
          },
          {
            contentToggle: false,
            folderName: 'freechart',
            imgCount: 4,
            content: {
              title: '프리차트(Freechart)',
              category: '개인 프로젝트',
              link: 'https://demain18.github.io/TeamFreeChart_client',
              github: 'https://github.com/demain18/TeamFreeChart_client',
              stack: [
                'React', 'Codeigniter', 'Mysql', 'AWS'
              ]
            }
          },
          {
            contentToggle: false,
            folderName: 'populer',
            imgCount: 7,
            content: {
              title: '포폴러(Populer)',
              category: '개인 프로젝트',
              link: null,
              github: null,
              stack: [
                'Javascript', 'Vue.js', 'Nuxt.js'
              ]
            }
          },
          {
            contentToggle: false,
            folderName: 'populer-intro',
            imgCount: 3,
            content: {
              title: '포폴러 소개',
              category: '개인 프로젝트',
              link: null,
              github: null,
              stack: [
                'Senmantic UI'
              ]
            }
          },
          {
            contentToggle: false,
            folderName: 'codingpack',
            imgCount: 8,
            content: {
              title: '코딩팩(CodingPack)',
              category: '개인 프로젝트',
              link: null,
              github: 'https://github.com/demain18/CodingPack',
              stack: [
                'Bootstrap', 'Jquery', 'PHP', 'Mysql'
              ]
            }
          },
          {
            contentToggle: false,
            folderName: 'bamin',
            imgCount: 8,
            content: {
              title: '배달의민족 PC 콘셉트',
              category: '개인 프로젝트',
              link: null,
              github: 'https://github.com/demain18/bamin_webconcept',
              stack: [
                'Bootstrap', 'Jquery'
              ]
            }
          },
          {
            contentToggle: false,
            folderName: 'twitter-clone',
            imgCount: 1,
            content: {
              title: '트위터 클론 코딩',
              category: '개인 프로젝트',
              link: null,
              github: null,
              stack: [
                //
              ]
            }
          },
          {
            contentToggle: false,
            folderName: 'pmarket',
            imgCount: 6,
            content: {
              title: 'Pmarket',
              category: '외주 프로젝트',
              link: null,
              github: null,
              stack: [
                'Vue.js', 'Vue CLI'
              ]
            }
          },
        ]
      },
      dialog: {
        on: false,
        index: 0,
      }
    }),
    mounted() {

    },
    methods: {
      langSelectClick() {
        //  this.$refs.langSelect.click()
      },
      eventHoverIn() {
        this.event.hover = true;
      },
      eventHoverOut() {
        this.event.hover = false;
      },
      projectContentToggle(mouse, index) {
        if (mouse=='in') {
          this.projectList.items[index].contentToggle = true;
        }
        else if (mouse=='out') {
          this.projectList.items[index].contentToggle = false;
        }
      },
      dialogToggle(index) {
        this.dialog.on = !this.dialog.on;
        this.dialog.index = index;
      },
      dialogClose(index) {
        this.dialog.on = false;
      }
    }
  }

</script>

<style>
  @import '~assets/css/basic.css';
  @import '~assets/css/basic.modal.css';
  @import '~assets/css/index.css';
  @import '~assets/css/index.mb.css';

</style>
