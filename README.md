import React, { useState, useEffect } from 'react';
import { 
  StyleSheet, 
  View, 
  Text, 
  ScrollView, 
  TouchableOpacity, 
  TextInput,
  Modal,
  SafeAreaView,
  StatusBar,
  Dimensions
} from 'react-native';
import { 
  Sprout, 
  Trophy, 
  Users, 
  Award, 
  MapPin, 
  Target, 
  Leaf, 
  Droplets, 
  Bug, 
  Sun, 
  Zap, 
  BookOpen, 
  Shield,
  CheckCircle, 
  Play, 
  Clock, 
  Star, 
  Share2, 
  Heart, 
  MessageCircle,
  ChevronRight, 
  Filter, 
  Search, 
  Gift, 
  Coins, 
  Sparkles,
  Bell,
  Image,
  Video
} from 'lucide-react-native';

const { width, height } = Dimensions.get('window');

export default function GreenQuestApp() {
  const [activeTab, setActiveTab] = useState('home');
  const [selectedMission, setSelectedMission] = useState(null);
  const [dailyLogin, setDailyLogin] = useState(false);
  const [searchQuery, setSearchQuery] = useState('');
  
  useEffect(() => {
    const lastLogin = localStorage.getItem('lastLogin');
    const today = new Date().toDateString();
    if (lastLogin !== today) {
      setDailyLogin(true);
      localStorage.setItem('lastLogin', today);
    }
  }, []);

  const farmerProfile = {
    name: "Rajesh Kumar",
    location: "Ludhiana, Punjab",
    farmSize: "5 acres",
    cropType: "Wheat & Rice",
    sustainabilityScore: 720,
    level: 8,
    badges: 12,
    streak: 21,
    coins: 450,
    experience: 1850,
    nextLevel: 2000
  };

  const missions = [
    {
      id: 1,
      title: "Mulch Master",
      description: "Apply organic mulch to 1 acre for 3 weeks",
      category: "Soil Health",
      icon: Leaf,
      progress: 65,
      xp: 150,
      coins: 75,
      duration: "3 weeks",
      impact: "Reduces water usage by 30%",
      color: "#10b981",
      difficulty: "Medium",
      steps: [
        "Collect organic mulch materials",
        "Apply 2-inch layer around crops",
        "Monitor soil moisture weekly",
        "Document results"
      ],
      resources: ["Mulching Guide", "Video Tutorial"]
    },
    {
      id: 2,
      title: "Bio-Warrior",
      description: "Switch to bio-pesticides for pest control",
      category: "Pest Management",
      icon: Bug,
      progress: 0,
      xp: 200,
      coins: 100,
      duration: "1 season",
      impact: "Eliminates chemical residue",
      color: "#3b82f6",
      difficulty: "Hard",
      steps: [
        "Identify local bio-pesticide sources",
        "Replace chemical pesticides",
        "Monitor pest population",
        "Compare crop health"
      ],
      resources: ["Bio-Pesticide Directory", "Expert Contact"]
    },
    {
      id: 3,
      title: "Water Wise",
      description: "Implement drip irrigation in 2 acres",
      category: "Water Conservation",
      icon: Droplets,
      progress: 100,
      xp: 250,
      coins: 125,
      duration: "Completed",
      impact: "Saves 40% irrigation water",
      color: "#06b6d4",
      difficulty: "Hard",
      steps: [
        "Survey land for irrigation layout",
        "Install drip irrigation system",
        "Calibrate water flow",
        "Measure water savings"
      ],
      resources: ["Installation Guide", "Subsidy Information"]
    },
    {
      id: 4,
      title: "Crop Diversity Champion",
      description: "Plant 3 different crops this season",
      category: "Mixed Cropping",
      icon: Sprout,
      progress: 33,
      xp: 300,
      coins: 150,
      duration: "1 season",
      impact: "Improves soil nutrients",
      color: "#22c55e",
      difficulty: "Medium",
      steps: [
        "Select complementary crops",
        "Plan crop rotation schedule",
        "Plant different crops",
        "Monitor soil health"
      ],
      resources: ["Crop Planning Tool", "Companion Planting Guide"]
    }
  ];

  const learningModules = [
    {
      id: 1,
      title: "Soil Health Basics",
      duration: "15 min",
      completed: true,
      type: "video"
    },
    {
      id: 2,
      title: "Organic Pest Control",
      duration: "20 min",
      completed: false,
      type: "article"
    },
    {
      id: 3,
      title: "Water Conservation",
      duration: "10 min",
      completed: false,
      type: "interactive"
    }
  ];

  const governmentSchemes = [
    {
      name: "PM-KUSUM Scheme",
      description: "Solar pump subsidy for irrigation",
      eligibility: "4+ eco-score required",
      deadline: "Dec 31, 2024",
      points: 50
    },
    {
      name: "Organic Certification",
      description: "Support for organic farming",
      eligibility: "Completed 5+ sustainable quests",
      deadline: "Rolling",
      points: 75
    }
  ];

  const leaderboard = [
    { rank: 1, name: "Harpreet Singh", score: 1240, village: "Jagraon", level: 15 },
    { rank: 2, name: "Amarjit Kaur", score: 980, village: "Khanna", level: 12 },
    { rank: 3, name: "Rajesh Kumar", score: 720, village: "Ludhiana", level: 8, isUser: true },
    { rank: 4, name: "Sukhdev Pal", score: 650, village: "Samrala", level: 7 },
    { rank: 5, name: "Parminder", score: 590, village: "Payal", level: 6 }
  ];

  const badges = [
    { name: "Water Saver", icon: Droplets, earned: true, description: "Saved 1000L water" },
    { name: "Organic Pro", icon: Leaf, earned: true, description: "3 organic quests completed" },
    { name: "Soil Guardian", icon: Sun, earned: true, description: "Improved soil health" },
    { name: "Community Leader", icon: Users, earned: false, description: "Help 5 farmers" },
    { name: "Eco Warrior", icon: Shield, earned: false, description: "Complete 10 quests" }
  ];

  const dailyQuests = [
    { title: "Check soil moisture", xp: 10, completed: true },
    { title: "Share progress", xp: 15, completed: false },
    { title: "Learn something new", xp: 20, completed: false }
  ];

  const ProgressBar = ({ progress, color, height = 8 }) => (
    <View style={[styles.progressBarContainer, { height }]}>
      <View 
        style={[
          styles.progressBar, 
          { 
            width: `${progress}%`,
            backgroundColor: color
          }
        ]} 
      />
    </View>
  );

  const MissionCard = ({ mission, onPress }) => {
    const Icon = mission.icon;
    return (
      <TouchableOpacity 
        style={styles.missionCard}
        onPress={() => onPress(mission)}
      >
        <View style={styles.missionHeader}>
          <View style={[styles.missionIcon, { backgroundColor: `${mission.color}20` }]}>
            <Icon size={24} color={mission.color} />
          </View>
          <View style={styles.missionInfo}>
            <View style={styles.missionTitleRow}>
              <Text style={styles.missionTitle}>{mission.title}</Text>
              <View style={[
                styles.difficultyBadge,
                { 
                  backgroundColor: 
                    mission.difficulty === 'Easy' ? '#dcfce7' :
                    mission.difficulty === 'Medium' ? '#fef9c3' :
                    '#fee2e2'
                }
              ]}>
                <Text style={[
                  styles.difficultyText,
                  {
                    color:
                      mission.difficulty === 'Easy' ? '#16a34a' :
                      mission.difficulty === 'Medium' ? '#ca8a04' :
                      '#dc2626'
                  }
                ]}>
                  {mission.difficulty}
                </Text>
              </View>
            </View>
            <Text style={styles.missionDescription}>{mission.description}</Text>
          </View>
        </View>
        
        <View style={styles.progressSection}>
          <View style={styles.progressLabels}>
            <Text style={styles.progressLabel}>Progress</Text>
            <Text style={styles.progressPercentage}>{mission.progress}%</Text>
          </View>
          <ProgressBar progress={mission.progress} color={mission.color} />
        </View>
        
        <View style={styles.missionFooter}>
          <View style={styles.rewards}>
            <Text style={styles.xpReward}>+{mission.xp} XP</Text>
            <View style={styles.coinReward}>
              <Coins size={14} color="#f59e0b" />
              <Text style={styles.coinText}>+{mission.coins}</Text>
            </View>
          </View>
          <View style={styles.missionMeta}>
            <Text style={styles.impact}>🌱 {mission.impact}</Text>
            <Text style={styles.duration}>⏱ {mission.duration}</Text>
          </View>
        </View>
      </TouchableOpacity>
    );
  };

  const renderHome = () => (
    <ScrollView style={styles.container} showsVerticalScrollIndicator={false}>
      {/* Daily Login Bonus */}
      {dailyLogin && (
        <View style={styles.dailyLoginCard}>
          <View style={styles.dailyLoginHeader}>
            <Gift size={24} color="#ffffff" />
            <Text style={styles.dailyLoginTitle}>Daily Login Bonus!</Text>
          </View>
          <Text style={styles.dailyLoginText}>+50 Coins & +25 XP for logging in today!</Text>
          <TouchableOpacity 
            style={styles.claimButton}
            onPress={() => setDailyLogin(false)}
          >
            <Text style={styles.claimButtonText}>Claim Reward</Text>
          </TouchableOpacity>
        </View>
      )}

      {/* Profile Header */}
      <View style={styles.profileCard}>
        <View style={styles.profileHeader}>
          <View>
            <Text style={styles.profileName}>{farmerProfile.name}</Text>
            <View style={styles.location}>
              <MapPin size={14} color="#d1fae5" />
              <Text style={styles.locationText}>{farmerProfile.location}</Text>
            </View>
            <Text style={styles.farmDetails}>
              {farmerProfile.farmSize} • {farmerProfile.cropType}
            </Text>
          </View>
          <View style={styles.levelBadge}>
            <Text style={styles.levelNumber}>Level {farmerProfile.level}</Text>
            <Text style={styles.levelLabel}>Eco Farmer</Text>
          </View>
        </View>
        
        {/* Progress Bar */}
        <View style={styles.levelProgress}>
          <View style={styles.progressLabels}>
            <Text style={styles.progressLabel}>Level Progress</Text>
            <Text style={styles.progressPercentage}>
              {farmerProfile.experience}/{farmerProfile.nextLevel} XP
            </Text>
          </View>
          <ProgressBar progress={(farmerProfile.experience / farmerProfile.nextLevel) * 100} color="#f59e0b" />
        </View>
        
        <View style={styles.statsGrid}>
          <View style={styles.statItem}>
            <Text style={styles.statNumber}>{farmerProfile.sustainabilityScore}</Text>
            <Text style={styles.statLabel}>Eco Score</Text>
          </View>
          <View style={styles.statItem}>
            <Text style={styles.statNumber}>{farmerProfile.badges}</Text>
            <Text style={styles.statLabel}>Badges</Text>
          </View>
          <View style={styles.statItem}>
            <Text style={styles.statNumber}>{farmerProfile.streak}🔥</Text>
            <Text style={styles.statLabel}>Streak</Text>
          </View>
          <View style={styles.statItem}>
            <View style={styles.coinStat}>
              <Coins size={16} color="#f59e0b" />
              <Text style={styles.statNumber}>{farmerProfile.coins}</Text>
            </View>
            <Text style={styles.statLabel}>Coins</Text>
          </View>
        </View>
      </View>

      {/* Daily Quests */}
      <View style={styles.dailyQuestCard}>
        <View style={styles.sectionHeader}>
          <Zap size={20} color="#f97316" />
          <Text style={styles.sectionTitle}>Daily Quests</Text>
        </View>
        <View style={styles.questList}>
          {dailyQuests.map((quest, idx) => (
            <View key={idx} style={styles.questItem}>
              <View style={styles.questInfo}>
                <View style={[
                  styles.questCheckbox,
                  quest.completed && styles.questCheckboxCompleted
                ]}>
                  {quest.completed && <CheckCircle size={14} color="#ffffff" />}
                </View>
                <Text style={[
                  styles.questTitle,
                  quest.completed && styles.questCompleted
                ]}>
                  {quest.title}
                </Text>
              </View>
              <Text style={styles.questXP}>+{quest.xp} XP</Text>
            </View>
          ))}
        </View>
      </View>

      {/* Active Missions */}
      <View style={styles.section}>
        <View style={styles.sectionHeaderRow}>
          <Text style={styles.sectionTitle}>Your Quests</Text>
          <View style={styles.sectionActions}>
            <TouchableOpacity style={styles.iconButton}>
              <Filter size={16} color="#6b7280" />
            </TouchableOpacity>
            <TouchableOpacity>
              <Text style={styles.viewAllText}>View All</Text>
            </TouchableOpacity>
          </View>
        </View>
        
        <View style={styles.missionsList}>
          {missions.map(mission => (
            <MissionCard 
              key={mission.id} 
              mission={mission} 
              onPress={setSelectedMission}
            />
          ))}
        </View>
      </View>

      {/* Learning Modules */}
      <View style={styles.section}>
        <View style={styles.sectionHeader}>
          <BookOpen size={20} color="#3b82f6" />
          <Text style={styles.sectionTitle}>Learn & Grow</Text>
        </View>
        <View style={styles.learningList}>
          {learningModules.map(module => (
            <TouchableOpacity key={module.id} style={styles.learningItem}>
              <View style={styles.learningIcon}>
                <View style={[
                  styles.learningIconCircle,
                  module.completed ? styles.learningCompleted : styles.learningPending
                ]}>
                  {module.completed ? 
                    <CheckCircle size={20} color="#16a34a" /> : 
                    <Play size={20} color="#3b82f6" />
                  }
                </View>
              </View>
              <View style={styles.learningContent}>
                <Text style={styles.learningTitle}>{module.title}</Text>
                <View style={styles.learningMeta}>
                  <Clock size={12} color="#6b7280" />
                  <Text style={styles.learningDuration}>{module.duration}</Text>
                  <Text style={styles.learningType}>{module.type}</Text>
                </View>
              </View>
              <ChevronRight size={20} color="#9ca3af" />
            </TouchableOpacity>
          ))}
        </View>
      </View>
    </ScrollView>
  );

  const renderLeaderboard = () => (
    <ScrollView style={styles.container} showsVerticalScrollIndicator={false}>
      <View style={styles.leaderboardHeader}>
        <Trophy size={48} color="#ffffff" />
        <Text style={styles.leaderboardTitle}>Panchayat Champions</Text>
        <Text style={styles.leaderboardSubtitle}>Compete with farmers in your region</Text>
      </View>

      {/* Search and Filter */}
      <View style={styles.searchSection}>
        <View style={styles.searchContainer}>
          <Search size={16} color="#6b7280" />
          <TextInput
            style={styles.searchInput}
            placeholder="Search farmers..."
            value={searchQuery}
            onChangeText={setSearchQuery}
          />
        </View>
        <TouchableOpacity style={styles.filterButton}>
          <Filter size={20} color="#6b7280" />
        </TouchableOpacity>
      </View>

      <View style={styles.leaderboardList}>
        {leaderboard.map(entry => (
          <View 
            key={entry.rank}
            style={[
              styles.leaderboardItem,
              entry.isUser && styles.userLeaderboardItem
            ]}
          >
            <View style={[
              styles.rankCircle,
              entry.rank === 1 && styles.firstRank,
              entry.rank === 2 && styles.secondRank,
              entry.rank === 3 && styles.thirdRank
            ]}>
              <Text style={[
                styles.rankText,
                entry.rank <= 3 && styles.topRankText
              ]}>
                {entry.rank === 1 ? '🥇' : entry.rank === 2 ? '🥈' : entry.rank === 3 ? '🥉' : entry.rank}
              </Text>
            </View>
            
            <View style={styles.leaderboardInfo}>
              <View style={styles.leaderboardNameRow}>
                <Text style={styles.leaderboardName}>{entry.name}</Text>
                {entry.isUser && (
                  <View style={styles.userBadge}>
                    <Text style={styles.userBadgeText}>You</Text>
                  </View>
                )}
              </View>
              <Text style={styles.leaderboardVillage}>{entry.village}</Text>
              <Text style={styles.leaderboardLevel}>Level {entry.level}</Text>
            </View>
            
            <View style={styles.leaderboardScore}>
              <Text style={styles.scoreNumber}>{entry.score}</Text>
              <Text style={styles.scoreLabel}>Eco Points</Text>
            </View>
          </View>
        ))}
      </View>

      {/* Government Schemes */}
      <View style={styles.schemesCard}>
        <View style={styles.sectionHeader}>
          <Award size={20} color="#3b82f6" />
          <Text style={styles.sectionTitle}>Available Schemes</Text>
        </View>
        <View style={styles.schemesList}>
          {governmentSchemes.map((scheme, idx) => (
            <View key={idx} style={styles.schemeItem}>
              <View style={styles.schemeHeader}>
                <Text style={styles.schemeName}>{scheme.name}</Text>
                <View style={styles.schemePoints}>
                  <Text style={styles.pointsText}>+{scheme.points} pts</Text>
                </View>
              </div>
              <Text style={styles.schemeDescription}>{scheme.description}</Text>
              <View style={styles.schemeMeta}>
                <Text style={styles.schemeEligibility}>🏆 {scheme.eligibility}</Text>
                <Text style={styles.schemeDeadline}>📅 {scheme.deadline}</Text>
              </View>
            </View>
          ))}
        </View>
      </View>
    </ScrollView>
  );

  const renderCommunity = () => (
    <ScrollView style={styles.container} showsVerticalScrollIndicator={false}>
      <View style={styles.communityHeader}>
        <Users size={48} color="#ffffff" />
        <Text style={styles.communityTitle}>Farmer Community</Text>
        <Text style={styles.communitySubtitle}>Share progress & learn together</Text>
      </View>

      {/* Create Post */}
      <View style={styles.createPostCard}>
        <View style={styles.createPostHeader}>
          <View style={styles.userAvatar}>
            <Text style={styles.avatarText}>{farmerProfile.name.charAt(0)}</Text>
          </View>
          <TouchableOpacity style={styles.postInput}>
            <Text style={styles.postInputText}>Share your farming journey...</Text>
          </TouchableOpacity>
        </View>
        <View style={styles.postActions}>
          <TouchableOpacity style={styles.postAction}>
            <Image size={16} color="#6b7280" />
            <Text style={styles.postActionText}>Photo</Text>
          </TouchableOpacity>
          <TouchableOpacity style={styles.postAction}>
            <Video size={16} color="#6b7280" />
            <Text style={styles.postActionText}>Video</Text>
          </TouchableOpacity>
          <TouchableOpacity style={styles.postAction}>
            <Award size={16} color="#6b7280" />
            <Text style={styles.postActionText}>Achievement</Text>
          </TouchableOpacity>
        </View>
      </View>

      {/* Community Posts */}
      <View style={styles.postsList}>
        {[
          {
            name: "Harpreet 
