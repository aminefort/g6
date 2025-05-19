<script setup>
import { fetchNui } from '../../utils';
import { useGlobalState } from '../../stores/globalStore';
import locale from "../../locale";

const globalState = useGlobalState();    

const jobFeatures = [
    {
        icon: 'pi pi-dollar',
        title: locale('home', 'features.competitive_pay.title'),
        description: locale('home', 'features.competitive_pay.description')
    },
    {
        icon: 'pi pi-clock',
        title: locale('home', 'features.flexible_hours.title'),
        description: locale('home', 'features.flexible_hours.description')
    },
    {
        icon: 'pi pi-chart-line',
        title: locale('home', 'features.career_growth.title'),
        description: locale('home', 'features.career_growth.description')
    },
    {
        icon: 'pi pi-users',
        title: locale('home', 'features.team_environment.title'),
        description: locale('home', 'features.team_environment.description')
    }
];

const CreateJob = async () => {
    const result = await fetchNui('create-job');
    globalState.pageData.value.current = result;
    globalState.changeCurrentTab('start-job');
}

const GetGroups = () => {
    globalState.changeCurrentTab('join-group');
    fetchNui('get-groups');
}
</script>

<template>
    <div class="home-container">
        <!-- Actions Section -->
        <div class="actions-sidebar">
            <div class="action-card">
                <div class="card-header">
                    <div class="header-icon">
                        <i class="pi pi-user-plus"></i>
                    </div>
                    <div class="header-content">
                        <h3>{{ locale('home', 'start_solo_job') }}</h3>
                        <p>{{ locale('home', 'group_job_description') }}</p>
                    </div>
                </div>
                <div class="card-actions">
                    <Button class="action-button" @click="CreateJob()">
                        <i class="pi pi-play"></i>
                        <span>{{ locale('home', 'start_job') }}</span>
                    </Button>
                </div>
            </div>

            <div class="action-card">
                <div class="card-header">
                    <div class="header-icon">
                        <i class="pi pi-users"></i>
                    </div>
                    <div class="header-content">
                        <h3>{{ locale('home', 'join_group_title') }}</h3>
                        <p>{{ locale('home', 'groups_description') }}</p>
                    </div>
                </div>
                <div class="card-actions">
                    <Button class="action-button secondary" @click="GetGroups()">
                        <i class="pi pi-search"></i>
                        <span>{{ locale('home', 'join_group') }}</span>
                    </Button>
                </div>
            </div>
        </div>

        <!-- Main Content Section -->
        <div class="main-content">
            <div class="content-header">
                <div class="header-icon">
                    <i class="pi pi-briefcase"></i>
                </div>
                <div class="header-text">
                    <h2>{{ locale('home', 'job_header_title') }}</h2>
                    <p>{{ locale('home', 'features.description') }}</p>
                </div>
            </div>

            <div class="features-grid">
                <div v-for="feature in jobFeatures" 
                     :key="feature.title" 
                     class="feature-item">
                    <div class="feature-icon">
                        <i :class="feature.icon"></i>
                    </div>
                    <div class="feature-content">
                        <h3>{{ feature.title }}</h3>
                        <p>{{ feature.description }}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.home-container {
    display: flex;
    gap: 2vh;
    padding: 2vh;
    height: 100%;
    width: 100%;
    color: white;
    min-height: 52vh;
    max-height: 52vh;

    .actions-sidebar {
        display: flex;
        flex-direction: column;
        gap: 2vh;
        width: 30vh;

        .action-card {
            background: rgba(22, 27, 34, 0.95);
            border: 1px solid rgba(0, 209, 245, 0.2);
            border-radius: 12px;
            padding: 2vh;
            display: flex;
            flex-direction: column;
            gap: 2vh;
            backdrop-filter: blur(10px);
            height: calc(50% - 1vh);

            .card-header {
                display: flex;
                gap: 1.5vh;
                align-items: flex-start;
                flex: 1;

                .header-icon {
                    width: 4.5vh;
                    height: 4.5vh;
                    min-width: 4.5vh;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    background: rgba(0, 209, 245, 0.1);
                    border: 2px solid rgba(0, 209, 245, 0.2);
                    border-radius: 8px;
                    transition: all 0.3s ease;

                    i {
                        font-size: 2vh;
                        color: #00D1F5;
                    }
                }

                .header-content {
                    flex: 1;
                    
                    h3 {
                        margin: 0;
                        font-size: 1.6vh;
                        color: #00D1F5;
                    }

                    p {
                        margin: 0.5vh 0 0;
                        font-size: 1.2vh;
                        color: rgba(255, 255, 255, 0.6);
                        line-height: 1.6vh;
                    }
                }
            }

            .card-actions {
                .action-button {
                    width: 100%;
                    height: 4vh;
                    border: none;
                    border-radius: 8px;
                    font-weight: 600;
                    font-size: 1.3vh;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    gap: 1vh;
                    transition: all 0.3s ease;
                    background: #00D1F5;
                    color: white;

                    &:hover {
                        background: darken(#00D1F5, 5%);
                        transform: translateY(-2px);
                    }

                    &.secondary {
                        background: rgba(0, 209, 245, 0.1);
                        border: 1px solid rgba(0, 209, 245, 0.2);
                        color: #00D1F5;

                        &:hover {
                            background: rgba(0, 209, 245, 0.15);
                        }
                    }

                    i {
                        font-size: 1.4vh;
                    }
                }
            }
        }
    }

    .main-content {
        flex: 1;
        background: rgba(22, 27, 34, 0.95);
        border: 1px solid rgba(0, 209, 245, 0.2);
        border-radius: 12px;
        padding: 2vh;
        display: flex;
        flex-direction: column;
        gap: 2vh;
        backdrop-filter: blur(10px);

        .content-header {
            display: flex;
            align-items: center;
            gap: 1.5vh;
            padding-bottom: 2vh;
            border-bottom: 1px solid rgba(0, 209, 245, 0.1);

            .header-icon {
                width: 5vh;
                height: 5vh;
                display: flex;
                align-items: center;
                justify-content: center;
                background: rgba(0, 209, 245, 0.1);
                border: 2px solid rgba(0, 209, 245, 0.2);
                border-radius: 8px;

                i {
                    font-size: 2.2vh;
                    color: #00D1F5;
                }
            }

            .header-text {
                h2 {
                    margin: 0;
                    font-size: 2vh;
                    color: #00D1F5;
                }

                p {
                    margin: 0.5vh 0 0;
                    font-size: 1.2vh;
                    color: rgba(255, 255, 255, 0.6);
                }
            }
        }

        .features-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 2vh;
            padding: 1vh;
            overflow-y: auto;
            flex: 1;

            &::-webkit-scrollbar {
                width: 4px;
            }

            &::-webkit-scrollbar-track {
                background: rgba(0, 209, 245, 0.05);
            }

            &::-webkit-scrollbar-thumb {
                background: rgba(0, 209, 245, 0.3);
                border-radius: 4px;
            }

            .feature-item {
                display: flex;
                gap: 1.5vh;
                padding: 2vh;
                background: rgba(0, 209, 245, 0.05);
                border: 1px solid rgba(0, 209, 245, 0.1);
                border-radius: 8px;
                transition: all 0.3s ease;
                height: fit-content;

                &:hover {
                    background: rgba(0, 209, 245, 0.08);
                    border-color: rgba(0, 209, 245, 0.2);
                    transform: translateX(4px);
                }

                .feature-icon {
                    width: 4vh;
                    height: 4vh;
                    min-width: 4vh;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    background: rgba(0, 209, 245, 0.1);
                    border: 2px solid rgba(0, 209, 245, 0.2);
                    border-radius: 8px;

                    i {
                        font-size: 1.8vh;
                        color: #00D1F5;
                    }
                }

                .feature-content {
                    flex: 1;
                    
                    h3 {
                        margin: 0;
                        font-size: 1.4vh;
                        color: white;
                    }

                    p {
                        margin: 0.5vh 0 0;
                        font-size: 1.2vh;
                        color: rgba(255, 255, 255, 0.6);
                        line-height: 1.6vh;
                    }
                }
            }
        }
    }
}
</style>