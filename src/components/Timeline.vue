<template>
  <div class="timeline">
    <div v-for="(person, i) in sortedTimeline" class="container" :key="i" :class="(i%2) === 0 ? 'left' : 'right'">
        <div class="circle" :class="(i % 2) === 0 ? 'on-left' : 'on-right'"></div>
        <div class="content">
            <img src="../assets/account.png" alt="Account Icon" class="img-icon">
            <div class="date">
                {{
                    dateForShow(person).getDate()
                }}
                {{
                    fullMonthNames[dateForShow(person).getMonth()]
                }}
                {{
                    dateForShow(person).getFullYear()
                }}
            </div>
            <div class="name">
                {{
                    person.name.first
                }}
                {{
                    person.name.last
                }}
            </div>
        </div>
    </div>
    <div class="circle-end"></div>
  </div>
</template>

<script setup>
import timeline from '../assets/timeline.json';

const sortedTimeline = timeline.sort((a,b) => new Date(a.registered) - new Date(b.registered));

const dateForShow = (i) =>  new Date(i.registered);

const fullMonthNames = [
    "January",
    "February",
    "March",
    "April",
    "May",
    "June",
    "July",
    "August",
    "September",
    "October",
    "November",
    "December"
]
</script>

<style lang="scss">
$blue-color: #364569;
$background: #dadada;

* {
    box-sizing: border-box;
}

body {
    background-color: $background;
    font-family: Helvetica, sans-serif;
}

.timeline {
    position: relative;
    max-width: 1200px;
    margin: 0 auto;
    /* circle on start */
    &::before {
            content: '';
            background-color: $blue-color;
            height: 20px;
            width: 20px;
            border-radius: 20px;
            position: absolute;
            top: 1px;
            left: 50%;
            margin-left: -10px;
        }
    /* line */
    &::after {
        content: '';
        position: absolute;
        width: 6px;
        background-color: $blue-color;
        top: 20px;
        bottom: 0;
        left: 50%;
        margin-left: -3px;
    }
}

.circle-end {
    background-color: $blue-color;
    height: 20px;
    width: 20px;
    border-radius: 20px;
    position: absolute;
    left: 48.5%;
    bottom: -10px;
}

.container {
    padding: 10px 20px;
    position: relative;
    background-color: inherit;
    width: 50%;
    top: 20px;
    /* circles on timeline */
    &::after {
        content: '';
        position: absolute;
        width: 15px;
        height: 15px;
        right: -11.5px;
        background-color: $background;
        border: 4px solid $blue-color;
        top: 60px;
        border-radius: 50%;
        z-index: 1;
    }
}

.left {
    left: 0;
    /* small lines */
    &::before {
        content: '';
        width: 70px;
        border-bottom: solid 5px $blue-color;
        position: absolute;
        right: 0;
        top: 70px;
        z-index: 1;
    }
}

.right {
    left: 50%;
    &::before {
        content: '';
        width: 70px;
        border-bottom: solid 5px $blue-color;
        position: absolute;
        left: 0;
        top: 70px;
        z-index: 1;
    }
    &::after {
        left: -12px;
    }
}

/* circles on the end of point */
.circle {
    background-color: $blue-color;
    height: 20px;
    width: 20px;
    border-radius: 20px;
    position: absolute;
    top: 62px;
}

.on-left {
    right: 60px;
}
.on-right {
    left: 60px;
}

.content {
    padding: 20px 20px;
    text-align: center;
    background-color: transparent;
    position: relative;
    border-radius: 20px;
    margin: 20px 20px;
}

.img-icon {
    width: 40px;
}
.date {
    font-weight: 600;
    font-size: 20px;
    color: $blue-color;
}
.name {
    font-size: 18px;
    color: #333;
}

@media screen and (max-width: 600px) {

    .timeline {
        /*line*/
        &::after {
            left: 31px;
        }
        /* start circle */
        &::before {
            content: '';
            background-color: $blue-color;
            height: 20px;
            width: 20px;
            border-radius: 20px;
            position: absolute;
            top: 4px;
            left: 31px;
            margin-left: -10px;
        }
    }

    .container {
        width: 100%;
        padding-left: 70px;
        padding-right: 25px;
        &::before {
            left: 30px;
            width: 70px;
            border-bottom: solid 5px $blue-color;
            position: absolute;
            top: 70px;
            z-index: 1;
        }
    }

    /* cirle on the end of point */
    .circle {
        background-color: $blue-color;
        height: 20px;
        width: 20px;
        border-radius: 20px;
        position: absolute;
        top: 63px;
        left: 88px;
    }

    .circle-end {
        background-color: $blue-color;
        height: 20px;
        width: 20px;
        border-radius: 20px;
        position: absolute;
        left: 21px;
        bottom: -10px;
    }

    .left::after, .right::after {
        left: 19px;
    }

    .right {
        left: 0%;
    }
}



</style>