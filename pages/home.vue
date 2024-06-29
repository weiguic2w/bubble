<template>
  <div class="fl-center" style="flex-direction: column">
    <div
      v-for="article in data"
      :key="article.time"
      style="border-bottom: 1px solid var(--bg-300)"
    >
      <div class="time">
        {{ article.time }}
      </div>
      <ul class="group">
        <li
          v-for="item in article.links"
          :key="item.to"
          class="article tooltip"
        >
          <nuxt-link
            :to="item.to"
            :class="{ active: $route.path.startsWith(item.to) }"
          >
            <h1>{{ item.title }}</h1>
            <p style="font-size: 1.6rem">{{ item.subtitle }}</p>
            <span class="tooltiptext">{{ item.cn_title }}</span>
          </nuxt-link>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: [
        {
          time: "2024-07",
          links: [
            {
              to: "/2024-07/0",
              title: "How Hamas Ends",
              subtitle: "A Strategy for Letting the Group Defeat Itself",
              cn_title: "哈马斯如何终结？",
            },
            {
              to: "/2024-07/1",
              title: "The Progressive Case for American Power",
              subtitle: "Retrenchment Would Do More Harm Than Good",
              cn_title: "进步派论美国实力",
            },
            {
              to: "/2024-07/2",
              title: "The Credibility Trap",
              subtitle: "Is Reputation Worth Fighting For?",
              cn_title: "信誉陷阱",
            },
            {
              to: "/2024-07/3",
              title: "Why They Don't Fight",
              subtitle: "The Surprising Endurance of the Democratic Peace",
              cn_title: "他们为什么不打",
            },
            {
              to: "/2024-07/4",
              title: "Why Would Anyone Want to Run the World?",
              subtitle: "The Warnings in Cold War History",
              cn_title: "谁会想统治世界？",
            },
            {
              to: "/2024-07/5",
              title: "Secular Stagnation",
              subtitle: "How Religion Endures in a Godless Age",
              cn_title: "世俗停滞",
            },
          ],
        },
        {
          time: "2024-06",
          links: [
            {
              to: "/2024-06/0",
              title: "War Unbound",
              subtitle: "Gaza, Ukraine, and the Breakdown of International Law",
              cn_title: "战争的约束",
            },
            {
              to: "/2024-06/1",
              title: "Iran's Order of Chaos",
              subtitle: "How the Islamic Republic Is Remaking the Middle East",
              cn_title: "伊朗的混乱秩序",
            },
            {
              to: "/2024-06/2",
              title: "Israel's Forever War",
              subtitle:
                "The Long History of Managing—Rather Than Solving—the Conflict",
              cn_title: "以色列的永恒战争",
            },
            {
              to: "/2024-06/3",
              title: "Spy and Tell",
              subtitle:
                "The Promise and Peril of Disclosing Intelligence for Strategic Advantage",
              cn_title: "告密者",
            },
            {
              to: "/2024-06/4",
              title: "All Powers Great and Small",
              subtitle: "Why Bigger Isn't Always Better in Geopolitics",
              cn_title: "大小权力",
            },
            {
              to: "/2024-06/5",
              title: "Tyrants of Industry",
              subtitle: "Can the Right Tame Capitalism?",
              cn_title: "产业暴君",
            },
            {
              to: "/2024-06/6",
              title: "The Leaning Tower of Babel",
              subtitle: "What We Lose When Languages Die",
              cn_title: "巴别塔之傾",
            },
          ],
        },
      ],
      darkTheme: false,
    };
  },
};
</script>

<style >
.group {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(700px, 1fr));
}
@media (max-width: 700px) {
  .group {
    grid-template-columns: 1fr; /* 在屏幕宽度小于700px时，将列数设为1 */
  }
}
.nuxt-link-active {
  border-bottom: 2px solid;
  color: var(--text-200);
}
.time {
  text-align: center;
  font-size: 1.8rem;
  margin-top: 2rem;
}
.article {
  padding: 1rem 2rem;
  border-radius: 0.2rem;
  transition: box-shadow 150ms ease-in-out;
}
.article:hover {
  box-shadow: 0 0 0 1px #ccc;
}
</style>
